# Technical Design (SDD)

**Owner:** Sara · **Status:** Reviewed

## 1. Drivers and boundaries

- Scope: R1–R4 and the workflows in [02](02-workflows-and-ui.md).
- Main design drivers: one part-time developer, under $25/month, strict per-user privacy, no lost edits (R3) — see [01](01-requirements.md).
- Exclusions: sharing, notifications, offline use, public API.

## 2. Architecture and stack choices

| Decision | Chosen option | Realistic alternatives | Why it fits; cost or limitation |
| --- | --- | --- | --- |
| Architecture | Single full-stack web app (one deployable) | Separate SPA + API | One codebase and deploy for one developer; would need splitting only if other clients appear. |
| Frontend / backend | Next.js (App Router) with server actions, TypeScript | React SPA + Express | Server-side ownership checks live next to the UI; the developer already knows React. |
| Data storage | PostgreSQL (managed) with Prisma | SQLite, MongoDB | Relational ownership and row-level conditional updates; see [ADR 001](decisions/001-use-postgresql.md). |
| Hosting / integrations | Vercel + Neon Postgres; Resend for sign-in email | Single VPS | Free/low tiers fit the budget; no server maintenance. Limitation: vendor-specific deployment. |

## 3. Components and runtime

- Diagram: Browser → Next.js app (Vercel) → Postgres (Neon). Next.js → Resend for email. Trust boundary: everything from the browser is untrusted.
- Responsibilities: `auth` module issues and verifies sign-in links and sessions; `tasks` module owns all reads and writes of the `tasks` table; `admin` module owns `invites`.
- Critical request — edit title: browser sends `{taskId, title, version}` → session resolves `userId` → validate title 1–200 chars → `UPDATE tasks SET title, version = version + 1 WHERE id = taskId AND owner_id = userId AND version = submitted AND status = 'open'` → 1 row: return updated task; 0 rows: re-read to return 404 (not owner / missing) or 409 (stale or completed).

## 4. Data and integrity

- Model: `users(id, email unique, role)`, `invites(email unique, invited_by)`, `tasks(id, owner_id → users, title, status, version, created_at, completed_at)`.
- Constraints and indexes: `CHECK (status IN ('open','completed'))`; `CHECK (char_length(title) BETWEEN 1 AND 200)`; index `(owner_id, status, created_at DESC)` for the list query.
- Atomic changes: each action is a single-row conditional update, so no multi-statement transaction is needed in release 1.
- Concurrency and retries: optimistic locking with `version` (R3). Create requests carry a client-generated `id`; inserting an existing ID is ignored, so a double submit creates one task.
- Data lifecycle: Prisma migrations applied in CI before deploy. No hard deletes; member deletion on request removes their user and tasks in one transaction.

## 5. Interfaces

| Operation / endpoint / event | Request and response | Authorization and validation | Expected errors / retry behavior |
| --- | --- | --- | --- |
| `createTask` | `{id: uuid, title}` → task | Signed in; title 1–200 | 400 invalid title; safe to retry with the same `id` |
| `updateTitle` | `{taskId, title, version}` → task | Owner; task open; version matches | 404 not found / not owner; 409 stale or completed — reload |
| `setStatus` | `{taskId, status}` → task | Owner | 404; repeating the same status is a no-op |
| `requestSignIn` | `{email}` → 202 | Rate limit 5/hour per email and IP | Always 202 to avoid revealing invited emails |

## 6. Security, failure handling, and deployment

- Identity and sessions: single-use sign-in links valid for 15 minutes; HTTP-only, Secure, SameSite=Lax session cookie, 30-day expiry. Every server action re-checks ownership in the query itself.
- Untrusted inputs and sensitive data: titles validated server-side and rendered as text (React escaping). Logs record user ID and task ID, never titles or emails.
- Dependency failure: database timeout of 5 s returns a retryable error to the UI; email send failures are logged and the user can request another link.
- Runtime topology: Vercel preview deployments use a separate Neon staging branch; production uses its own database. Secrets live in Vercel environment variables.
- Operability: p95 list latency and error rate come from Vercel analytics; procedures are in [06](06-release-and-operations.md).

## 7. Risks and unresolved decisions

| Risk / unknown | Impact | Evidence, experiment, or mitigation | Owner / needed before |
| --- | --- | --- | --- |
| Sign-in emails land in spam | Users cannot sign in | Deliverability test with 3 staff inboxes; fallback: admin-generated one-time link | Sara / slice 1 |
| List query slow at 2,000 tasks | Misses performance target | Seed staging with 2,000 tasks and measure | Sara / release |

## Ready to implement the first slice

- [x] Its components, data changes, and interfaces are specified.
- [x] Its permission rules and critical integrity/failure/concurrency behavior have an implementation approach.
- [x] Choices fit the expected workload, budget, and operating capabilities.
- [x] Its important assumptions are tested and verification is planned in 05.

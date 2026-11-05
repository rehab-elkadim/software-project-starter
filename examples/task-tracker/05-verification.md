# Verification (Test Plan)

**Release / build:** 1.0.0-rc.1 (commit `a1b2c3d`) · **Environment:** Staging (Vercel preview + Neon staging branch) · **Owner:** Sara

## 1. Scope and approach

- In scope: R1–R4, ownership isolation, conflict handling, performance at 2,000 tasks.
- Outside this check: load beyond 15 users (not expected); email client rendering beyond Gmail and Outlook web.
- Test setup: seeded users `member-a`, `member-b`, `admin` on staging; seed script adds 2,000 tasks to `member-a`.
- Automated checks: unit tests for validation; integration tests against a test database for every server action, including ownership and version checks; Playwright end-to-end tests for the create/complete and edit-conflict workflows. All run in CI on every PR.
- Manual/user acceptance checks: keyboard-only pass and 360 px layout (Sara); two team members complete a day of real tasks on staging.

## 2. Important scenarios

| Requirement / risk | Starting condition and action | Expected result | Test / evidence link | Result |
| --- | --- | --- | --- | --- |
| R2 | Signed in → submit title "Write brief" | One open task at the top of the list | `e2e/create-complete.spec.ts`, CI run | Pass |
| R2 | Double-press Enter on one title | Exactly one task exists | `tasks.integration.test.ts › idempotent create` | Pass |
| R3 | Open task in two tabs → edit in tab 1 → edit in tab 2 | Tab 2 shows conflict; tab 1's title kept | `e2e/edit-conflict.spec.ts` | Pass |
| Access | `member-b` calls `updateTitle` with `member-a`'s task ID | 404; task unchanged | `tasks.integration.test.ts › ownership` | Pass |
| R1 | Uninvited email requests a link | Same message as invited; no email sent | `auth.integration.test.ts` + Resend log | Pass |
| Performance | `member-a` (2,000 tasks) loads list, 50 runs | p95 under 1 s | k6 run on staging, report link | Pass (p95 410 ms) |
| Accessibility | Complete R2–R4 using keyboard only | All actions reachable, focus visible | Manual, 2026-11-03 | Pass |

## 3. Defects and accepted limitations

| Issue | Impact | Blocks release? | Resolution or explicit acceptance by / reason |
| --- | --- | --- | --- |
| #14 Completed list not paginated | Slow scroll past ~5,000 completed tasks | No | Accepted by Sara: no user will reach that in year 1; revisit at 3-month review |

## Release decision

- [x] Critical workflow, access-control, and data-integrity checks pass for the release candidate.
- [x] Relevant quality targets are demonstrated, with material environment limitations stated.
- [x] No launch-blocking defects remain; remaining issues have an explicit disposition.
- [x] Representative users have verified their intended tasks where user acceptance applies.
- Decision: Go — Sara — 2026-11-04 — 1.0.0-rc.1

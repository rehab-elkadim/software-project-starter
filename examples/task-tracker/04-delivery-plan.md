# Delivery Plan (Implementation Plan)

**Release:** 1.0 — personal task lists · **Owner:** Sara · **Target:** 4 weeks, part-time

## 1. Build order

| Order | Slice / demonstrable outcome | Requirements | Dependencies / prerequisites | Issues / completion evidence |
| --- | --- | --- | --- | --- |
| 1 | An invited member signs in, creates a task, and still sees it after reloading | R1, R2 | Repo, CI, staging database, email provider account | #1–#5; demo recording, CI run |
| 2 | Member completes and reopens tasks | R4 | Slice 1 | #6–#7 |
| 3 | Member edits a title with conflict protection | R3 | Slice 1 | #8–#9 |
| 4 | Admin invites a new member | R1 (invites) | Slice 1 | #10 |

## 2. First implementation tasks

Slice 1 issues, each created from the feature template:

- #1 Project setup: Next.js, lint/typecheck/test in CI, Vercel staging deployment.
- #2 Database schema and first migration for `users`, `invites`, `tasks`.
- #3 Email sign-in with single-use links and sessions.
- #4 Create task with idempotent ID and validation.
- #5 Task list (open section) with loading, empty, and error states.

## 3. Release confidence

- Expected finish / estimate: 3–5 weeks, assuming about 10 hours a week and no change to scope.
- External blocker or schedule risk: email deliverability (#3) — Sara — test in week 1.
- Demo / feedback plan: two team members use staging at the end of weeks 2 and 4 and manage a real day's tasks.

## Definition of done for a slice

- [ ] Acceptance criteria are demonstrated, including important failure/permission cases.
- [ ] Relevant automated checks pass; manual checks have recorded results.
- [ ] The change has been reviewed, or self-reviewed for a solo project.
- [ ] Necessary migrations, configuration, and documentation are included.
- [ ] It works in the agreed integration/staging environment.

## Ready to start

- [x] The next slice and its issues are small enough to implement and review.
- [x] Its required decisions, access, and dependencies are available.

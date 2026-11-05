# Delivery plan

**Release:** [Name / scope] · **Owner:** [Name] · **Target:** [Date or explicitly unknown]

Keep tasks and their live status in your issue tracker. This page explains the release slices and their order.

## 1. Build order

Each slice should deliver demonstrable behavior across the necessary UI, API, and data changes. Foundation work is allowed where a slice actually needs it.

| Order | Slice / demonstrable outcome | Requirements | Dependencies / prerequisites | Issues / completion evidence |
| --- | --- | --- | --- | --- |
| 1 | [First usable workflow] | [IDs or links] | [Setup, decision, or external access] | [Issue links; add demo/test evidence as completed] |
| 2 | [Next outcome] | [IDs or links] | [What must work first] | [Links] |

> Example: A user signs in, creates a task, and sees it after reloading. Its completion includes UI, authorization, persistence, error handling, and verification.

## 2. First implementation tasks

Create feature issues using the repository template. Each issue should state the intended outcome, bounded scope, acceptance criteria, and meaningful verification. Link it above; avoid maintaining a second task list here.

For the first slice, include only the required repository/runtime setup, migration, CI checks, and staging deployment work. Choose the stack first.

## 3. Release confidence

- Expected finish / estimate: [Range and assumptions if a date matters; otherwise N/A]
- External blocker or schedule risk: [Issue link, owner, and next action]
- Demo / feedback plan: [Who tries the slice and what task they perform]

## Definition of done for a slice

- [ ] Acceptance criteria are demonstrated, including important failure/permission cases.
- [ ] Relevant automated checks pass; manual checks have recorded results.
- [ ] The change has been reviewed, or self-reviewed for a solo project.
- [ ] Necessary migrations, configuration, and documentation are included.
- [ ] It works in the agreed integration/staging environment.

## Ready to start

- [ ] The next slice and its issues are small enough to implement and review.
- [ ] Its required decisions, access, and dependencies are available.


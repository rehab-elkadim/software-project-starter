# Requirements (PRD)

**Project:** [Name] · **Owner:** [Who resolves scope/rules] · **Status:** [Draft / Agreed]

Fill before selecting the implementation. Keep implementation choices in the technical design.

## 1. Problem and desired outcome

- Users: [Who uses this and what they need to accomplish]
- Current problem: [What happens today; why that causes difficulty]
- Desired outcome: [What should improve]
- Success measure: [Observed baseline, target, and how/when it will be measured; mark an unknown baseline explicitly]

## 2. First release and constraints

- Included: [Small set of complete user outcomes]
- Excluded / later: [Explicit boundaries]
- Constraints: [Time, budget, team capabilities, platforms, and external dependencies that affect feasibility]

## 3. Required behavior

| ID | User outcome / required behavior | Acceptance criteria |
| --- | --- | --- |
| R1 | [Who can accomplish what] | [Given a relevant starting condition, when an action occurs, what observable result follows?] |

> Example: R1 — A signed-in user creates a task. With a nonempty title, saving creates one task visible in their list; a blank title is rejected without creating a record.

## 4. Business rules

List rules that must always hold, including ownership, editing, uniqueness, history, and exceptional actions. Put role-by-role access and state transitions in [workflows](02-workflows-and-ui.md).

- [Rule and any permitted exception]

## 5. Quality and data requirements

| Area | Required outcome and acceptance condition |
| --- | --- |
| Access and privacy | [Who may access which data; sensitive fields; retention/deletion obligations and decision owner] |
| Performance and capacity | [Expected usage/data volume; latency or throughput target under a defined workload] |
| Availability and recovery | [Acceptable downtime and data loss; required restoration time, if relevant] |
| Usability and compatibility | [Devices, browsers, languages, accessibility needs, and how to verify them] |

Use project-specific targets. Record an assumption if a number is estimated, including how it will be checked.

## 6. Open questions and dependencies

| Question / assumption / dependency | Owner | Resolution or next check | Needed before |
| --- | --- | --- | --- |
| [What remains unknown] | [Name] | [Evidence or decision needed] | [Affected design/work] |

## Ready to design the first slice

- [ ] Its user outcome, scope, rules, and acceptance criteria are agreed.
- [ ] Its access, data, and quality constraints are explicit.
- [ ] Unknowns that could invalidate that slice are resolved or have a tested fallback.


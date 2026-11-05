# Requirements (PRD)

**Project:** Task Tracker · **Owner:** Sara (product and scope) · **Status:** Agreed

## 1. Problem and desired outcome

- Users: members of a 5–15 person agency team who each manage their own work items.
- Current problem: tasks live in a shared spreadsheet; people overwrite each other's rows and cannot tell what is done.
- Desired outcome: each member keeps a private, reliable list of open and completed tasks.
- Success measure: within 4 weeks of launch, at least 80% of the team (baseline 0) creates a task in the app at least 3 days a week, measured from the `tasks.created_at` timestamps.

## 2. First release and constraints

- Included: email sign-in, create / edit / complete / reopen own tasks, list of open and completed tasks.
- Excluded / later: sharing or assigning tasks, due-date reminders, mobile app, file attachments.
- Constraints: one developer, 4 weeks part-time, hosting budget under $25/month, desktop and mobile browsers.

## 3. Required behavior

| ID | User outcome / required behavior | Acceptance criteria |
| --- | --- | --- |
| R1 | A team member signs in with their work email | Given an invited email, when the user follows the emailed link, they reach their task list; an uninvited email receives no sign-in link and sees the same neutral message. |
| R2 | A signed-in member creates a task | With a title of 1–200 characters, saving creates exactly one open task shown at the top of their list; a blank or longer title is rejected with a message and nothing is created. |
| R3 | A member edits the title of their open task | Saving a valid title updates it; if the task changed since it was loaded, the save is refused and the user is shown the current version. |
| R4 | A member completes or reopens a task | Completing moves it to the completed list with a completion time; reopening returns it to the open list and clears the time. |

## 4. Business rules

- A task belongs to exactly one member; only that member can see or change it.
- Completed tasks cannot be edited until reopened.
- Tasks are not hard-deleted in the first release; history is kept for the success measure.
- Only an admin can invite a new email address.

## 5. Quality and data requirements

| Area | Required outcome and acceptance condition |
| --- | --- |
| Access and privacy | Task titles are visible only to their owner. Stored data: email, task title, timestamps. A member's data is deleted within 30 days of an admin request; Sara owns that decision. |
| Performance and capacity | Up to 15 users and 20,000 tasks. Task list loads in under 1 s (p95) for a user with 2,000 tasks on a staging database of that size. |
| Availability and recovery | Business-hours tool: up to 4 h downtime is acceptable; at most 24 h of data loss; restore within 4 h. |
| Usability and compatibility | Current Chrome, Safari, Firefox, Edge; 360 px wide screens; keyboard-operable forms, checked with axe and a manual keyboard pass. English only. |

The 2,000-tasks-per-user figure is an estimate (about 10 tasks a day for a year); it will be checked against real usage after 3 months.

## 6. Open questions and dependencies

| Question / assumption / dependency | Owner | Resolution or next check | Needed before |
| --- | --- | --- | --- |
| Can the agency's mail domain receive transactional email without spam filtering? | Sara | Send test sign-in links to 3 staff inboxes | Slice 1 (sign-in) |
| Do people want due dates in release 1? | Sara | Ask in week-2 demo | Release 2 planning |

## Ready to design the first slice

- [x] Its user outcome, scope, rules, and acceptance criteria are agreed.
- [x] Its access, data, and quality constraints are explicit.
- [ ] Unknowns that could invalidate that slice are resolved or have a tested fallback. — mail deliverability test pending

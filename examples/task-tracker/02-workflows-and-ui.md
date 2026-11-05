# Workflows and UI (User Flows & Wireframes)

**Owner:** Sara · **Status:** Reviewed

Wireframes are low-fidelity frames in the project's design file; frame names are given below.

## 1. Domain terms and lifecycle

- Terms: **Member** — an invited person with their own list. **Admin** — a member who can also invite people.
- Main objects: a Member owns many Tasks.
- Lifecycle: `open ⇄ completed`. A task starts `open`.

| From → to | Action | Who may do it | Preconditions / prohibited transitions |
| --- | --- | --- | --- |
| (none) → open | Create | Any member | Valid title |
| open → completed | Complete | Task owner | Task is open |
| completed → open | Reopen | Task owner | Task is completed |
| open → open | Edit title | Task owner | Task is open; version matches (R3). Editing a completed task is prohibited. |

## 2. Permissions

| Actor / role | Record and field visibility | Allowed actions | Conditions / exceptions |
| --- | --- | --- | --- |
| Member | Own tasks only, all fields | Create, edit, complete, reopen | Ownership checked on every request; a guessed task ID returns "not found". |
| Admin | Own tasks; list of invited emails | Member actions + invite email | Admins cannot see other members' tasks. |
| Signed-out visitor | Nothing | Request a sign-in link | Response is identical for invited and uninvited emails. |

## 3. Critical workflow

### Create and complete a task — R2, R4

- Actor and starting condition: a signed-in member on the task list.
- Normal path: 1. Type a title in "New task". 2. Press Enter or "Add". 3. The task appears at the top of Open. 4. Tick its checkbox. 5. It moves to Completed with the time shown.
- Result: one task exists in state `completed` with `completed_at` set.
- Alternate / failure paths: blank title → inline "Enter a title", focus stays in the field. Double-pressing Enter → still one task. Network failure → the row shows "Not saved — Retry" and the typed title is kept. Session expired → redirect to sign-in, then back to the list.
- Wireframes: `List / default`, `List / save-failed`.

### Edit a title — R3

- Actor and starting condition: the owner of an open task.
- Normal path: 1. Click the title. 2. Change it. 3. Press Enter.
- Result: the new title is shown and saved.
- Alternate / failure paths: task changed in another tab → "This task changed elsewhere" with the current title loaded; the user's text is kept in the field so it can be re-applied. Task completed elsewhere → edit closes and the task moves to Completed.
- Wireframes: `List / editing`, `List / conflict`.

## 4. Screen behavior

| Screen | Main action and fields | Loading / empty / error / success behavior | Wireframe |
| --- | --- | --- | --- |
| Sign in | Email field, "Send link" | After submit: "If this email is invited, a link is on its way." Expired link: "This link has expired" + send-again button. | `Sign in / *` |
| Task list | New-task field; Open and Completed sections; checkbox and editable title per row | Loading: 5 skeleton rows. Empty: "No tasks yet — add your first one above." Load error: message + Retry. | `List / *` |
| Invite (admin) | Email field, "Invite" | Duplicate email: "Already invited". Success: email added to the list below. | `Admin / invite` |

On screens under 600 px the Completed section is collapsed by default.

## Ready to implement a workflow

- [x] Its starting conditions, transitions, and permissions are unambiguous.
- [x] Someone can follow the normal and important failure paths through the wireframes.
- [x] The screen behavior matches the requirements and technical design.

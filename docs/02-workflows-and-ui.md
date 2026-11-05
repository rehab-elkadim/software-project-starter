# Workflows and UI

**Owner:** [Name] · **Status:** [Draft / Reviewed]

Describe user-visible behavior here. Link wireframes from any tool; polished visual design is not required before proving the workflow.

## 1. Domain terms and lifecycle

- Terms: [Only concepts with a project-specific meaning]
- Main objects: [What users work with and how the objects relate]
- Lifecycle: [Text or diagram showing the meaningful states and allowed transitions]

| From → to | Action | Who may do it | Preconditions / prohibited transitions |
| --- | --- | --- | --- |
| [State → state] | [Action] | [Role plus ownership/scope] | [Rules] |

## 2. Permissions

Describe both the action and which records/fields it applies to. List privileged exceptions explicitly.

| Actor / role | Record and field visibility | Allowed actions | Conditions / exceptions |
| --- | --- | --- | --- |
| [Role] | [Own records / assigned records / specific fields] | [Actions] | [Ownership, state, and other limits] |

> Example: Member — sees their own tasks; can update the title only while the task is open. Guessing another task's ID grants no access.

## 3. Critical workflow

Repeat this short block for each distinct workflow in the first release.

### [Workflow name — related requirement IDs]

- Actor and starting condition: [Who, where, and required state]
- Normal path: [Numbered steps or linked flowchart]
- Result: [Observable outcome and final state]
- Alternate / failure paths: [Validation, denied access, missing/stale data, interruption, or duplicate submission where relevant; say what the user sees and can do next]
- Wireframes: [Link to screens with stable names or frame IDs]

## 4. Screen behavior

List distinct screens. Include only relevant states; attach responsive/accessibility notes where behavior changes.

| Screen | Main action and fields | Loading / empty / error / success behavior | Wireframe |
| --- | --- | --- | --- |
| [Name] | [Inputs and actions] | [Concrete display and recovery behavior] | [Link] |

## Ready to implement a workflow

- [ ] Its starting conditions, transitions, and permissions are unambiguous.
- [ ] Someone can follow the normal and important failure paths through the wireframes.
- [ ] The screen behavior matches the requirements and technical design.


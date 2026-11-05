# Software Project Starter

A reusable, stack-neutral documentation kit for taking an application from idea to production. The overall process is the software development life cycle (SDLC).

Designed for a solo engineer or a small team building a web application. Expand it when integrations, multiple teams, formal approvals, or other project constraints require more detail. It is a practical starting point, not a compliance specification.

## Reuse for each project

1. Make this repository a GitHub **Template repository** in its settings.
2. For a new project, use **Use this template → Create a new repository**. Each project gets independent history and its own filled documents.
3. Clone the new project repository. Replace the README placeholders, fill the documents progressively, and add the application code here or link its separate repository.
4. Keep the starter's placeholders clean; put project-specific answers in that project's copy. Copies do not automatically receive future template updates.

For an existing application, copy `docs/` and the desired GitHub templates into its repository and reconcile its existing README. Preserve existing files and conventions.

## The six working documents

| Document | When to use it | Enough detail means |
| --- | --- | --- |
| 01 Requirements | Before choosing the implementation | Users, scope, rules, quality targets, and observable acceptance criteria are clear. |
| 02 Workflows and UI | Before implementing an affected workflow | States, permissions, screens, and important failure behavior agree. |
| 03 Technical design | Before committing to significant technical choices | Stack and boundaries have reasons; data integrity, access, and critical failure/concurrency cases have a design. |
| 04 Delivery plan | Before starting implementation | The first usable slice, its dependencies, and its completion criteria are explicit. |
| 05 Verification | Start during design; add evidence during implementation | Critical requirements have relevant checks and release evidence for the actual version. |
| 06 Release and operations | Sketch during design; complete before launch | Deployment, migrations, detection, rollback, and restoration have actionable, verified procedures. |

Use these in loops. For each new feature, update affected requirements/design, implement a small slice, verify it, and update operating instructions if needed. The sequence is not a requirement to finish all documentation before writing code.

## Keep the work proportional

- Answer each prompt with a concrete project-specific fact, rule, decision, or link. One sentence is often enough.
- Example rows marked **Example** illustrate the expected specificity. Replace them; they are not decisions for your project.
- Keep one authoritative location for each fact. Reference requirements from tickets; link actual API contracts and automated tests instead of copying them.
- Use `N/A — reason` for inapplicable sections and `TBD — owner — needed by` for unanswered questions. A placeholder is not a completed answer.
- Resolve unknowns before the work that depends on them. A future feature's unanswered question need not block unrelated work.
- Update documents in the same PR as behavior or design changes. Git history records previous versions.
- Write an optional [decision record](docs/decisions/ADR-TEMPLATE.md) when a consequential choice needs its own discussion. Small choices can stay in the design document.

The templates combine the brief with the PRD, combine workflows with UI references, and combine release with operations. A separate SRS, HLD, LLD, or test-strategy document can be added if a specific audience or project obligation needs it.

## Implementation support

GitHub feature and bug issue templates are in `.github/ISSUE_TEMPLATE/`. A PR template helps describe the behavior change and its verification. Use your issue tracker as the task list; the delivery document only records release slices and ordering.

No application stack, build pipeline, coverage percentage, or service-level target is imposed. Choose them from the project's requirements. Plan tests around risk and observable behavior.

## Sources and further reading

These are original, condensed templates informed by the following resources. This kit is not an official template from any of those organizations.

- [Atlassian PRD](https://www.atlassian.com/software/confluence/templates/product-requirements)
- [Chromium DevTools design documentation](https://chromium.googlesource.com/devtools/devtools-frontend/+/ef4afa3c0171a5b55f494947f5adf684b2cdac1a/docs/contributing/design.md)
- [arc42 architecture overview](https://arc42.org/overview/)
- [MADR decision records](https://adr.github.io/madr/)
- [GitHub issue templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)
- [TestRail test planning](https://www.testrail.com/blog/create-a-test-plan/)
- [Make a README](https://www.makeareadme.com/)
- [Atlassian operations runbook](https://www.atlassian.com/software/confluence/templates/devops-runbook)
- [GitHub template repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)


# Software Project Starter

Reusable Markdown templates for the **Software Development Life Cycle (SDLC)**, from understanding an idea to launching and operating the software.

Use this repository when you want a practical structure for documenting what to build, how it should work, how to implement it, and what evidence makes it ready to ship. It is designed for solo developers and small teams, especially those building web applications.

## What is included

| Stage | Document | Purpose |
| --- | --- | --- |
| 1 | [Requirements (PRD)](docs/01-requirements.md) | Product Requirements Document: define the problem, scope, rules, and acceptance criteria. |
| 2 | [Workflows and UI (User Flows & Wireframes)](docs/02-workflows-and-ui.md) | Define user journeys, permissions, state changes, and screen behavior. |
| 3 | [Technical Design (SDD)](docs/03-technical-design.md) | Software Design Document: explain architecture, stack choices, data, APIs, security, and failure handling. |
| 4 | [Delivery Plan (Implementation Plan)](docs/04-delivery-plan.md) | Organize usable increments, dependencies, and implementation tickets. |
| 5 | [Verification (Test Plan)](docs/05-verification.md) | Define checks, record results, and assess release readiness. |
| 6 | [Release and Operations (Release Plan & Runbook)](docs/06-release-and-operations.md) | Document deployment, migrations, monitoring, rollback, and restoration. |

Also included: GitHub feature/bug issue templates, a pull-request template, and an optional [Architecture Decision Record (ADR)](docs/decisions/ADR-TEMPLATE.md).

See [examples/task-tracker](examples/task-tracker/README.md) for all six documents filled in for a small sample project.

## How to use it

1. Click **Use this template → Create a new repository**, then clone your new repository.
2. Replace its README with the project README template below and fill in your project details.
3. Work through the documents as decisions become relevant. Each stage includes prompts, examples, and a readiness checklist.
4. Add your application code and update the affected documents alongside implementation changes.

For an existing application, copy the documents and the GitHub templates you need into its repository.

Keep answers specific and brief. Link code, diagrams, tickets, and tests rather than duplicating them. Revisit earlier stages when new information changes the design.

Read [START-HERE.md](START-HERE.md) for the full workflow, guidance on keeping documentation proportional, and source references.

## Project README template

Copy the following into your application's README after creating a project from this starter.

````markdown
# [Project name]

[One sentence: what this application does and who uses it.]

**Status:** [Planning / Building / Live]  
**Maintainer:** [Name or team]  
**Application:** [URL, or not deployed]

> Starting a new project? Read [START-HERE.md](START-HERE.md), then replace the brackets in this README. Remove this note afterward.

## Run locally

- Prerequisites: [Runtime and version, package manager, required services]
- Install: `[command]`
- Configure: [Where to find the environment-variable example and local service setup]
- Database setup / migrations: `[command, or N/A]`
- Start: `[command]`
- Local address: [URL]

Document variable names and where to obtain values; keep credentials outside Git.

## Checks

| Check | Command |
| --- | --- |
| Static checks | [Lint / typecheck command] |
| Tests | [Test command] |
| Production build | [Build command] |

## Project documentation

1. [Requirements: what and why](docs/01-requirements.md)
2. [Workflows and UI: behavior and screens](docs/02-workflows-and-ui.md)
3. [Technical design: how it works](docs/03-technical-design.md)
4. [Delivery plan: what to build next](docs/04-delivery-plan.md)
5. [Verification: what proves it works](docs/05-verification.md)
6. [Release and operations: how to ship and run it](docs/06-release-and-operations.md)

## Contributing

[How to pick up an issue, open a PR, and obtain review; for a solo project, state the checks required before merging.]

````

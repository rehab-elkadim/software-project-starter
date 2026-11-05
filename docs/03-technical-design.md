# Technical design

**Owner:** [Name] · **Status:** [Proposed / Reviewed / Implemented]

Design critical behavior before implementing it. Add detail for the next slice as needed; link contracts and schemas once they exist in code.

## 1. Drivers and boundaries

- Scope: [Which requirements/workflows this design addresses]
- Main design drivers: [The constraints and quality requirements that most affect the solution; link 01]
- Exclusions: [What this design deliberately leaves out]

## 2. Architecture and stack choices

| Decision | Chosen option | Realistic alternatives | Why it fits; cost or limitation |
| --- | --- | --- | --- |
| Architecture | [Application structure] | [Other viable structure] | [Requirement-specific tradeoff] |
| Frontend / backend | [Technologies] | [Viable alternatives] | [Reason] |
| Data storage | [Technology] | [Viable alternatives] | [Reason] |
| Hosting / integrations | [Services] | [Viable alternatives] | [Reason] |

Do not add infrastructure without a concrete need. Link a [decision record](decisions/ADR-TEMPLATE.md) if the reasoning grows beyond this table.

## 3. Components and runtime

- Diagram: [Browser/client, application modules, database, external systems; label communication and trust boundaries]
- Responsibilities: [Each significant module's job and who owns shared data]
- Critical request: [Trace one important operation through authorization, validation, persistence, and response; include external/background work only if used]

## 4. Data and integrity

- Model: [Entities/tables/collections, key fields, relationships, and ownership; link schema or ER diagram]
- Constraints and indexes: [Uniqueness, referential rules, and indexes justified by actual access patterns]
- Atomic changes: [Which writes must succeed/fail together and the transaction/alternative used]
- Concurrency and retries: [How stale writes, conflicting actions, and duplicate requests are handled where relevant]
- Data lifecycle: [How migrations/imports, history, retention, and deletion meet the requirements]

> Example: Update an item only if its stored version matches the submitted version. Return a conflict for a stale update; do not silently overwrite another user's work.

## 5. Interfaces

For the next slice, define requests, responses, validation, authorization, and failures. Once an OpenAPI specification or another contract exists, link it instead of duplicating it.

| Operation / endpoint / event | Request and response | Authorization and validation | Expected errors / retry behavior |
| --- | --- | --- | --- |
| [Method + path, or operation] | [Required fields, types, result] | [Role + record/field scope + business preconditions] | [Meaningful error and caller action] |

## 6. Security, failure handling, and deployment

- Identity and sessions: [Authentication/session design; authorization enforcement location]
- Untrusted inputs and sensitive data: [Relevant validation, abuse protection, browser protections, storage/transport controls, and safe logging]
- Dependency failure: [Timeouts, failure response, retry/idempotency strategy if applicable]
- Runtime topology: [What runs where, environment separation, configuration/secrets management, and supporting services]
- Operability: [How requirement targets are met and measured; link deployment/recovery procedures in 06]

## 7. Risks and unresolved decisions

| Risk / unknown | Impact | Evidence, experiment, or mitigation | Owner / needed before |
| --- | --- | --- | --- |
| [Specific uncertainty] | [What could fail] | [How it is resolved or bounded] | [Name / affected work] |

## Ready to implement the first slice

- [ ] Its components, data changes, and interfaces are specified.
- [ ] Its permission rules and critical integrity/failure/concurrency behavior have an implementation approach.
- [ ] Choices fit the expected workload, budget, and operating capabilities.
- [ ] Its important assumptions are tested and verification is planned in 05.


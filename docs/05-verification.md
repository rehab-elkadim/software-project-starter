# Verification

**Release / build:** [Version or commit] · **Environment:** [Where checked] · **Owner:** [Name]

Start during design. Record what could fail and how it will be checked. Add results for the actual release candidate; link existing tests and CI rather than rewriting them.

## 1. Scope and approach

- In scope: [Release workflows and highest-impact risks]
- Outside this check: [Exclusions and their reasons]
- Test setup: [Required services, test identities/roles, fixtures, and environment differences that affect confidence]
- Automated checks: [Test suites/commands/CI links and what each proves]
- Manual/user acceptance checks: [What requires a human and who performs it]

## 2. Important scenarios

Cover normal behavior and relevant denied access, invalid input, conflicting actions, retry/failure, migration, and recovery behavior. Add performance/accessibility checks when required by 01. Delete inapplicable example categories rather than claiming they were tested.

| Requirement / risk | Starting condition and action | Expected result | Test / evidence link | Result |
| --- | --- | --- | --- | --- |
| [R1 or risk] | [Precondition → action] | [Observable behavior] | [Automated test, CI run, or manual result] | [Not run / Pass / Fail / Blocked] |

> Example: Unauthorized access — user B requests user A's private item directly through the API. The response reveals no item data; the stored item is unchanged.

Measure quality targets using the workload and conditions defined in 01. A sample response time without a workload is not performance evidence.

## 3. Defects and accepted limitations

| Issue | Impact | Blocks release? | Resolution or explicit acceptance by / reason |
| --- | --- | --- | --- |
| [Link] | [Who/what is affected] | [Yes / No] | [Fix evidence, or named decision owner and rationale] |

## Release decision

- [ ] Critical workflow, access-control, and data-integrity checks pass for the release candidate.
- [ ] Relevant quality targets are demonstrated, with material environment limitations stated.
- [ ] No launch-blocking defects remain; remaining issues have an explicit disposition.
- [ ] Representative users have verified their intended tasks where user acceptance applies.
- Decision: [Go / No-go — decision owner — date — build reference]

Choose release criteria based on risk. A generic pass percentage or coverage number does not establish that critical behavior works.


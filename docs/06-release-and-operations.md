# Release and Operations (Release Plan & Runbook)

**Service / release:** [Name and version] · **Release owner:** [Name] · **Operations owner:** [Name]

Make these instructions executable by someone with the stated access. Reference approved configuration locations and variable names, never credential values.

## 1. Runtime and access

| Environment | Application / health URL | Hosting and data services | Configuration / access instructions |
| --- | --- | --- | --- |
| Staging | [URLs] | [Services] | [Location / required access] |
| Production | [URLs] | [Services] | [Location / required access] |

- Build/deploy mechanism: [CI workflow or exact commands; how the released commit/artifact is identified]
- First-launch data: [Import/migration/initial account setup, or N/A; include verification and reconciliation]

## 2. Release procedure

Replace every item below with the project's exact commands or linked procedures before launch.

1. Verify the release candidate's [test evidence](05-verification.md) and required access/configuration.
2. Check migration compatibility, pre-release backup/recovery point, and the rollback boundary.
3. Deploy the identified artifact and run migrations in the required order. State any downtime or staged rollout steps.
4. Run smoke checks: health, sign-in, and one critical read/write workflow. Use safe test data and specify cleanup.
5. Observe the named metrics/logs for the agreed window. Stop or roll back at the thresholds below.

- Project-specific commands / workflow links: [Fill]
- Smoke-check actions and expected results: [Fill]
- Observation window, signals, and rollback thresholds: [Fill]
- Last rehearsal: [Date, environment, build, result, evidence]

## 3. Rollback and data compatibility

- Trigger and decision owner: [When rollback is appropriate and who acts]
- Application rollback: [Exact artifact/version selection and commands]
- Database compatibility: [Whether the previous app works with the new schema; how to handle incompatible migrations]
- Recovery boundary: [Which writes/data changes rollback cannot undo; whether a forward fix or restore is needed]
- Verification after rollback: [Smoke checks and expected results]
- Last rollback rehearsal: [Date, environment, outcome, evidence]

Do not assume that redeploying old code reverses database changes or external side effects. Record the actual strategy.

## 4. Backups and restoration

- Backup source, frequency, retention, and access: [Fill; reconcile with data requirements]
- Recovery point / recovery time targets: [Link to 01]
- Restore procedure: [Exact steps, isolation from live traffic, and any reconciliation of writes after the backup]
- Integrity checks after restore: [How correctness and usability are verified]
- Last restore test: [Date, environment, measured recovery result, evidence]

## 5. Monitoring and incident response

| Signal / alert | Dashboard or log location | Trigger | First action / runbook |
| --- | --- | --- | --- |
| [Errors, latency, availability, data/queue health as relevant] | [Link] | [Threshold tied to expected operation] | [Concrete check and action] |

- Alert delivery and responsible person: [Channel and coverage arrangements]
- Escalation / user communication owner: [Who acts if first response fails]
- Known failure procedure: [Symptom → diagnosis → mitigation → recovery check; link longer procedures only if needed]

## Ready to launch

- [ ] Deployment and smoke checks have succeeded in a representative environment.
- [ ] Required production configuration/access and migration/import checks are ready.
- [ ] Applicable rollback and backup restoration procedures have been rehearsed.
- [ ] Alerts reach a responsible person and that person can access the runbook.
- [ ] Release thresholds, accepted limitations, and post-launch observation are agreed.


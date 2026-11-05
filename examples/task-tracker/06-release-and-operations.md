# Release and Operations (Release Plan & Runbook)

**Service / release:** Task Tracker 1.0.0 · **Release owner:** Sara · **Operations owner:** Sara

## 1. Runtime and access

| Environment | Application / health URL | Hosting and data services | Configuration / access instructions |
| --- | --- | --- | --- |
| Staging | `staging.tasks.example.com`, `/api/health` | Vercel preview, Neon `staging` branch, Resend test domain | Vercel project env "Preview"; access via team Vercel and Neon accounts |
| Production | `tasks.example.com`, `/api/health` | Vercel production, Neon `main` branch, Resend | Vercel env "Production"; variable names listed in `.env.example` |

- Build/deploy mechanism: merging to `main` runs CI, then `prisma migrate deploy`, then the Vercel production deploy. The release is the Git tag `v1.0.0`; Vercel shows the commit SHA.
- First-launch data: admin account created by `npm run seed:admin -- --email <admin email>`; verify by signing in. No data import.

## 2. Release procedure

1. Confirm the [verification](05-verification.md) Go decision for the tagged commit.
2. Create a Neon branch `pre-v1.0.0` from production as the recovery point. Release 1 migrations only add tables, so the previous app version stays compatible.
3. Merge the release PR; CI applies migrations, then deploys. No downtime expected.
4. Smoke checks (below) using the `smoke-test@example.com` account; complete its test task afterwards.
5. Watch errors and latency for 30 minutes.

- Project-specific commands / workflow links: `.github/workflows/deploy.yml`; manual fallback `npx prisma migrate deploy && vercel deploy --prod`.
- Smoke-check actions and expected results: `/api/health` returns 200 with `db: ok`; sign in via link; create "smoke <date>" and see it after reload; complete it.
- Observation window, signals, and rollback thresholds: 30 min; roll back if the 5xx rate is above 2% for 5 minutes or any smoke check fails.
- Last rehearsal: 2026-11-04, staging, rc.1, passed — CI run link.

## 3. Rollback and data compatibility

- Trigger and decision owner: any threshold above is crossed; Sara decides.
- Application rollback: Vercel → Deployments → previous production deployment → "Promote to Production".
- Database compatibility: release 1 migrations are additive; the previous version ignores new tables. Later destructive migrations must use expand-then-contract over two releases.
- Recovery boundary: tasks created after release remain in the database after an app rollback; that is the intended behavior. Emails already sent cannot be recalled.
- Verification after rollback: repeat the smoke checks.
- Last rollback rehearsal: 2026-11-04, staging, promoted the previous deployment in under 2 minutes; smoke checks passed.

## 4. Backups and restoration

- Backup source, frequency, retention, and access: Neon point-in-time restore, 7-day history; access through the team Neon account (Sara and one backup admin).
- Recovery point / recovery time targets: 24 h / 4 h — see [01 §5](01-requirements.md#5-quality-and-data-requirements).
- Restore procedure: create a Neon branch at the chosen timestamp; point the staging app at it and verify; then switch the production `DATABASE_URL` to the restored branch and redeploy. Tasks written after the restore point are exported from the old branch and re-inserted if needed.
- Integrity checks after restore: task count per user compared with the pre-incident query; smoke checks pass.
- Last restore test: 2026-11-04, staging, restored to 1 hour earlier in 12 minutes end to end; counts matched.

## 5. Monitoring and incident response

| Signal / alert | Dashboard or log location | Trigger | First action / runbook |
| --- | --- | --- | --- |
| Server errors | Vercel → Observability | 5xx above 2% for 5 min | Check logs for the failing action; roll back if it started with a deploy |
| Health check | Uptime monitor on `/api/health` | 2 consecutive failures, 1 min apart | Check Neon status, then Vercel status; post in team channel |
| Sign-in email failures | Resend dashboard | Any bounce spike or delivery below 95% in an hour | Check domain DNS (SPF/DKIM); give affected users an admin one-time link |

- Alert delivery and responsible person: email and phone push to Sara during business hours.
- Escalation / user communication owner: if Sara is unavailable, the backup admin posts status in the team channel and follows this runbook.
- Known failure procedure: "Users can't sign in" → check Resend delivery log → if the domain is failing verification, fix DNS → confirm by sending a link to a staff inbox.

## Ready to launch

- [x] Deployment and smoke checks have succeeded in a representative environment.
- [x] Required production configuration/access and migration/import checks are ready.
- [x] Applicable rollback and backup restoration procedures have been rehearsed.
- [x] Alerts reach a responsible person and that person can access the runbook.
- [x] Release thresholds, accepted limitations, and post-launch observation are agreed.

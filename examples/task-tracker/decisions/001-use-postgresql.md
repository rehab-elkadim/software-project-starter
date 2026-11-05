# Use PostgreSQL for task data

**Status:** Accepted · **Date:** 2026-10-20 · **Owner:** Sara

## Context

Tasks have strict per-user ownership (01 §4), edits must not overwrite newer changes (R3), and hosting must stay under $25/month for one part-time developer.

## Options

| Option | Advantages for this project | Costs / limitations |
| --- | --- | --- |
| PostgreSQL (managed, Neon) | Conditional single-row updates for optimistic locking; foreign keys and CHECK constraints enforce ownership and valid states; free tier and branch-based staging/restore | One more managed service to configure |
| SQLite (file on the app server) | Simplest setup, no network hop | Serverless hosting has no persistent disk; backups would be manual |
| MongoDB (managed) | Flexible documents | Ownership and state rules would live only in application code; no relational constraints |

## Decision and consequences

Use PostgreSQL on Neon with Prisma. Database constraints back up the application's rules, and Neon branches give cheap staging databases and point-in-time restores. We accept a dependency on Neon's availability and pricing; the schema uses standard PostgreSQL so it can move to another host.

## Revisit if

The team grows beyond about 200 users, sharing between members is added, or Neon's free tier no longer covers the expected storage.

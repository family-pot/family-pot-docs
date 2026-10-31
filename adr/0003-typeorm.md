# ADR 0003: TypeORM for database access

- Status: accepted
- Date: 2026-09-30

## Context
family-pot-api (NestJS) needs a PostgreSQL data layer with reproducible schema changes.
Contributors use their own local Postgres (for example via pgAdmin). The maintainer hosts the
shared database on Neon or Render. Docker is not required for contributors.

## Options considered
1. TypeORM (first-class NestJS integration)
2. Prisma
3. Drizzle

## Decision
TypeORM, configured from a single `DATABASE_URL`.

Rules:
- `synchronize` is always `false`. Schema changes go through migrations only.
- SSL is configurable by env (`DATABASE_SSL`), because Neon and Render require it.
- Destructive scripts (migration revert, test reset, seed) refuse to run unless the host is
  local, or `ALLOW_REMOTE_DB_RESET=true` is set explicitly.
- Tests use a separate `DATABASE_URL_TEST`, never the development database.
- Postgres `bigint` and `numeric` columns come back from the driver as strings. This is wanted
  for money and must not be cast to JavaScript numbers.

## Consequences
- Contributors need a local Postgres and a `DATABASE_URL`. No Docker.
- CI uses a GitHub Actions Postgres service container.
- TypeORM's migration generator can produce unexpected diffs, so every generated migration must
  be reviewed by hand in the PR.
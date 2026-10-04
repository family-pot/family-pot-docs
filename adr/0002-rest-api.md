# ADR 0002: REST API with NestJS

- Status: accepted
- Date: 2026-09-28

## Context

`family-pot-web` and `family-pot-api` are separate repos and need a defined API contract between
them. A backend framework and API style need to be chosen.

## Options considered

1. REST API built with NestJS.
2. GraphQL API.
3. tRPC (type-safe RPC, tightly coupled frontend/backend types).

## Decision

REST with NestJS. NestJS gives a structured, modular backend with built-in support for
validation, dependency injection, and OpenAPI/Swagger generation, which keeps the contract
between `family-pot-web` and `family-pot-api` explicit and documented. REST keeps the API
contract simple to version and consume for a project expecting many independent contributors
across two repos — GraphQL's flexibility and tRPC's tight coupling both add complexity not
needed at this stage.

## Consequences

- `family-pot-api` exposes versioned REST endpoints with generated Swagger docs at `/api/docs`.
- `family-pot-web` consumes the API over plain HTTP/REST — no shared-type package required
  across repos, which fits the poly-repo structure.
- Revisit if cross-repo type drift becomes a recurring problem; that would be a new ADR.
# ADR 0005: Authentication and ownership

- Status: proposed (maintainer decision needed on token transport)
- Date: 2026-09-30

## Context
The API will be hosted publicly (Render) with a shared database. Without authentication anyone
could read or write data. Web is hosted on Vercel, a different site from the API.

## Decision
- Email and password sign-up and login.
- Passwords hashed with argon2id. Never logged, never returned.
- Access token: JWT, 15 minutes.
- Refresh token: random opaque string, stored only as a hash, rotated on every use, with reuse
  detection (a reused token revokes the whole token family). Lifetime 7 days.
- Every user-owned table has a non-null `userId` foreign key. Every query is scoped to the
  authenticated user. Access to another user's record returns 404.
- Auth failures return generic messages (no "email not found" versus "wrong password").

## Open question: token transport (maintainer decides)
Recommended: refresh token in an httpOnly, Secure cookie; access token returned in JSON and
kept in memory by the web app; Vercel rewrites proxy `/api/*` to the Render API so cookies are
first-party. Alternative: bearer tokens stored by the client (simpler, more exposed to XSS).
The details of the Vercel proxy approach should be verified before implementing.

## Out of scope for now
Email verification, password reset, OAuth, MFA, account deletion.

## Consequences
Every later model carries `userId`. Security review is required for any change to auth code.
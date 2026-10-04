# Architecture

## Repository boundaries

Family Pot is split into four repositories:

| Repo | Responsibility |
| --- | --- |
| `family-pot-web` | Next.js UI. Calls `family-pot-api` over REST. No direct database access, no Stellar key handling. |
| `family-pot-api` | NestJS backend. Owns the database, business logic, and (from M4) read-only Stellar/Horizon calls and unsigned-transaction building. |
| `family-pot-contracts` | Reserved, inactive. Activates only per ADR 0001. |
| `family-pot-docs` | This repo. Single source of truth for product, architecture, roadmap, assumptions, threat model, and ADRs. |

Browser ──REST──> family-pot-web ──REST──> family-pot-api ──> PostgreSQL
│
└──> Stellar Horizon (read-only, from M4)


## Non-goals (shared across repos)

- Moving or holding money on the user's behalf
- Storing or handling any private/secret keys, in any repo
- Automatic recurring payments (reminders only, until auth, consent, and confirmation are
  designed and reviewed)
- Bank-account linking, live rate scraping, general FX calculator
- Acting as a regulated money-transfer service

## Money rules

- Amounts are stored as integer minor units plus an ISO 4217 (or asset) code — never a float.
- Exchange rates are decimal strings or a decimal type, never a JavaScript `number`.
- Rounding mode is explicit and documented per calculation.
- These rules apply in `family-pot-api` (source of truth) and in any display logic in
  `family-pot-web` that formats money.

## Data provenance

Every value shown to a user has exactly one provenance:

| Provenance | Meaning |
| --- | --- |
| `user-entered` | Typed in by the user |
| `calculated` | Derived deterministically from user-entered values |
| `estimated` | Based on documented assumptions — see `ASSUMPTIONS.md` |
| `verified` | Confirmed against the Stellar network by transaction lookup |

Estimated savings are never presented as guaranteed. The API returns provenance alongside every
financial figure; the frontend is responsible for displaying it visibly.

## Stellar

Claimable balances and payments are classic Stellar operations (`PaymentOp`,
`CreateClaimableBalanceOp`, `ClaimClaimableBalanceOp`), built with the Stellar JS SDK in
`family-pot-api`. No smart contract is required for the current roadmap — see ADR 0001.

Constraints confirmed from Stellar's own documentation that shape the design:

- The claimant must be a specific account, named at creation — there is no open "anyone with the
  link" claim without embedding a secret, which Family Pot will never do.
- For non-native assets, the claimant needs a trustline before claiming, or the claim fails.
- The creator's minimum reserve rises per claimant.
- Predicates (including time-based sender-reclaim windows) are evaluated at claim time against
  ledger close time — a claim valid in a preview can still fail at the deadline.
- An unclaimed balance cannot be deleted, so the sender is always included as a fallback claimant.
- This design does not work for authorization-required assets.

Conclusion: claimable balances do **not** provide a wallet-free experience. The recipient needs
a Stellar account, and for non-native assets a trustline. See `THREAT_MODEL.md` for the resulting
security rules and open questions.

## Decisions

Architecture decisions are recorded in `adr/`.
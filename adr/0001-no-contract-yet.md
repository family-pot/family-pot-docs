# ADR 0001: No smart contract yet

- Status: accepted
- Date: 2026-09-28

## Context

Family Pot's Stellar features — payment verification and, experimentally, claimable balances —
can be built with classic Stellar operations (`PaymentOp`, `CreateClaimableBalanceOp`,
`ClaimClaimableBalanceOp`) via the Stellar JS SDK. A `family-pot-contracts` repo is reserved but
currently empty.

## Options considered

1. No contract now; classic operations only, in `family-pot-api`.
2. Build a Soroban/Rust contract now, in `family-pot-contracts`, for claimable-balance logic.
3. Build a contract later, only if a specific requirement needs it.

## Decision

Option 1 combined with option 3's trigger condition. No contract is built now. None of the
current roadmap (M0–M5) requires logic beyond what classic operations and predicates express. A
contract adds audit surface and money-handling risk that isn't justified without a concrete
need.

`family-pot-contracts` stays reserved and empty. This decision is revisited specifically during
issue S1 (claimable balance research), and reopened if a concrete requirement appears — for
example, conditional multi-step claims, pooled/programmable family funds, or on-chain enforcement
of recurring-transfer logic — none of which are in scope today.

## Consequences

- Simpler contributor setup: three active repos instead of four.
- Any future contract work requires a new ADR describing the specific requirement, trade-offs,
  and a security review plan, approved by maintainers before implementation begins.
- `family-pot-contracts/README.md` states this status so contributors don't open implementation
  PRs there prematurely.
# Threat model (initial)

Status: **stub**, to be expanded by issue S4 before any Stellar transaction-building code is
merged in `family-pot-api`.

## Non-negotiable rules (apply to every repo)

1. Never request, store, log, or transmit a Stellar secret key.
2. Never put a secret key, or anything that grants spending power, in a URL or shareable link.
3. Never show a Stellar transfer as completed until it is verified on-chain.
4. Never fabricate exchange rates, fees, savings, or transaction statuses.
5. Signing always happens in the user's own wallet — `family-pot-api` builds unsigned
   transactions only.

## Assets to protect

- Users' transfer history and recipient details (personal and financial data), held in
  `family-pot-api`'s database
- Integrity of calculated and estimated figures shown in `family-pot-web`
- Correctness of claim predicates and reclaim windows once S5 is built

## Open questions (tracked by S1 and S4)

- **Claim flow:** the claimant account is fixed at creation — a "claim link" cannot be an
  open-to-anyone link without exposing a secret. Which recipient flow is acceptable given this?
  (Current direction: recipient supplies their public address before the sender signs.)
- **Expiry and reclaim:** sender is always a fallback claimant; time-based predicates are
  evaluated against ledger close time, so a UI preview can disagree with the on-chain result near
  a deadline. How should the UI communicate this uncertainty?
- **Trustlines and off-ramp:** does the launch corridor have a realistic anchor path from the
  Stellar asset to local currency? Unverified — part of S1.
- **Rate limiting / abuse:** what prevents spamming claimable-balance creation against
  `family-pot-api`? To be addressed in S5's design.

## Review process

Any PR touching `family-pot-api`'s Stellar code, or any `family-pot-contracts` work (if ever
activated), requires a security-focused review referencing this document before merge.
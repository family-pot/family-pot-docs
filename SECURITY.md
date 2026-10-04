# Security Policy

This is the shared security policy for all Family Pot repositories:

- [family-pot-web](https://github.com/family-pot/family-pot-web)
- [family-pot-api](https://github.com/family-pot/family-pot-api)
- [family-pot-contracts](https://github.com/family-pot/family-pot-contracts)
- [family-pot-docs](https://github.com/family-pot/family-pot-docs)

Family Pot deals with financial records and, from milestone M4 onward, Stellar transactions.

## Reporting a vulnerability

Please **do not** open a public issue. Use GitHub's private vulnerability reporting on the
affected repo, for example:
<https://github.com/family-pot/family-pot-api/security/advisories/new>

If you're unsure which repo is affected, report it against `family-pot-api`.

Include what you found, how to reproduce it, and the potential impact. We aim to acknowledge
reports within 5 working days. (Maintainers: replace this with a real contact and a response
commitment you can actually honour before launch.)

## Design principles (apply across all repos)

- No repo requests, stores, logs, or transmits a Stellar secret key. Signing happens only in the
  user's own wallet.
- A transfer is shown as completed on Stellar only after it has been verified on the network —
  never optimistically.
- Exchange rates, fees, savings, and transaction statuses are never fabricated. Estimates are
  always labelled as estimates, with assumptions documented in `ASSUMPTIONS.md`.
- Claimable-balance and any contract work must pass a security review before merging — see
  `THREAT_MODEL.md` and `family-pot-contracts/README.md`.

## Scope

In scope: code and configuration in the four repos listed above.
Out of scope: third-party services (Stellar Horizon, anchors, hosting providers) and the Stellar
network itself.
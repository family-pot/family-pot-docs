# Product Definition

## Problem statement

People who send money home to family regularly have no easy way to see the full picture of that
spending over time: how much they've sent in total, how much it has cost them in fees and rate
spread, and whether the route they use is actually competitive against alternatives. Each
transfer is usually a one-off interaction with a provider's app — there is no running history,
no trend, and no honest cost comparison across providers or time.

## Target users

People and families who send money across borders on a recurring basis — not occasional or
one-time senders, but people who do this monthly or regularly to support family members abroad.
Family Pot is deliberately general across corridors and currencies rather than built around one
specific country pair.

## Core use cases

1. **Track who I send money to.** Create recipients (e.g. "Mum — Nigeria") and record transfers
   to them over time.
2. **See the full history.** View every transfer with its date, amount, currency, rate, fee,
   provider, purpose, status, and notes.
3. **Understand the real cost.** See lifetime totals, total fees paid, average transfer size,
   and monthly trends — without having to recompute any of it by hand.
4. **Compare routes honestly.** Compare actual historical cost against another provider or a
   hypothetical Stellar route, with the estimate clearly labelled and its assumptions documented.
5. **Remember recurring transfers.** Set up a recurring transfer (recipient, amount, frequency)
   and get reminded when the next one is due, without the app moving money automatically.
6. **Export records.** Export transfer history as CSV for personal record-keeping.

## What Family Pot is not

- Not a money-transfer service. It does not move funds on the user's behalf.
- Not a custodian. It never holds funds or handles private/secret keys.
- Not a general-purpose FX calculator or price-comparison site unrelated to the user's own
  transfers.
- Not an automatic-payment system. Recurring transfers are reminders, not standing instructions,
  until authentication, authorization, consent, and transaction confirmation are properly
  designed and reviewed.
- Not a regulated financial institution and does not claim to be one.

## Why this is different from existing tools

Generic personal-finance trackers log spending but have no concept of a "remittance route," fee
structure, or cross-currency rate. Provider apps (Remitly, FamEx, etc.) show only their own
transfers, with no way to compare against other providers or to see a lifetime view across
providers. Family Pot sits specifically at the intersection of recurring remittance tracking and
honest cost comparison — a gap not covered by either category. See `ARCHITECTURE.md` for how
this is reflected in scope, and `ASSUMPTIONS.md` for how comparison estimates are kept honest.

## Non-goals

See `MVP.md` for the MVP scope and `ARCHITECTURE.md` for the full non-goals list shared with the
engineering docs.
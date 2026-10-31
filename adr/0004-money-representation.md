# ADR 0004: Money representation

- Status: proposed
- Date: 2026-09-30

## Context
Money and exchange rates must never use floating point.

## Decision
**Amounts** are integer minor units plus an ISO 4217 code. In code: `bigint`. In the database:
`bigint`. On the wire (JSON): the amount is a string.

    { "amount": "15000", "currency": "GBP" }   // £150.00

**Exchange rates** are decimal strings (units of receiving currency per 1 unit of sending
currency). Database: `numeric(24,12)`. On the wire: string, for example `"1950.5"`.

**Conversion** from minor units of currency A to minor units of currency B:

    result = amountMinor x rate x 10^(exponentB - exponentA), then rounded

with a decimal library (decimal.js) for the multiplication. The rounding mode is always an
explicit argument. Default for user-facing conversion: round half up. Ties-to-even is available.

**Fees** are in the sending currency. **Currency exponents** come from a constant table
(JPY 0, GBP 2, KWD 3 and so on). MVP currencies: GBP, USD, EUR, CAD, NGN, GHS, KES, INR, PHP.

## Worked examples
1. £150.00 at 1950.5 NGN per GBP: 15000 x 1950.5 = 29257500 kobo, which is NGN 292,575.00.
2. 1001 pence x 1.2345 = 1235.7345, rounds (half up) to 1236, which is 12.36.
3. Tie: 5 x 0.5 = 2.5. Half up gives 3; half to even gives 2.

## Consequences
- No `number` arithmetic on money anywhere (API or web).
- Both repos can implement this independently. Reconciling differences is part of the later
  "connect web to API" issues.
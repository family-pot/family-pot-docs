# MVP

The MVP is tracking-first. It does not move money and does not automate anything financial.

## In scope

### Recipients

- Create, edit, and delete a recipient (e.g. "Mum — Nigeria")
- A recipient has at minimum a name and a location/country

### Transfers

Users can record a transfer to a recipient with the following fields:

- Date
- Amount
- Sending currency
- Receiving currency
- Exchange rate
- Fee
- Provider
- Purpose
- Status
- Notes

Transfers can be created, edited, and deleted. Every stored value is `user-entered` unless
explicitly derived — see `ARCHITECTURE.md` for the provenance model.

### Transfer history

- List of all transfers for a recipient and across all recipients
- Filterable (by recipient, date range, provider, status at minimum)

### Dashboard

- Total amount sent
- Number of transfers
- Total fees paid
- Average transfer amount
- Monthly totals
- Cumulative amount sent over time
- Cost trends

Charts are added only where they answer a specific, useful question — not by default.

### Cost comparison

- Compare actual historical cost (what the user actually paid) against another provider or a
  hypothetical Stellar route
- Actual cost and estimated/hypothetical cost are visually and textually distinguished at all
  times
- Estimated savings are never presented as guaranteed
- Every comparison calculation documents its assumptions in `ASSUMPTIONS.md`

### Recurring transfers (reminders only)

- Define a recurring transfer: recipient, amount, frequency, next due date
- Get reminded when a transfer is due
- Marking a reminder as sent creates a real transfer record
- No automatic money movement. Authentication, authorization, consent, and transaction
  confirmation are explicitly out of scope until designed and reviewed separately.

### Export

- Export transfer history as CSV

## Explicitly out of scope for MVP

- Any Stellar functionality (payments, verification, claimable balances) — see the roadmap;
  these begin at milestone M4, after the MVP
- Automatic/standing payments
- Bank account linking
- Live exchange rate feeds
- Multi-user accounts, sharing, or family-member logins
- Mobile apps (web only for MVP)
- Notifications beyond in-app reminders (e.g. email/push) — tracked separately in the roadmap

## Definition of done for the MVP

- A user can create a recipient, record several transfers to them with all listed fields, see
  the dashboard update correctly, run a cost comparison with assumptions visible, set up a
  recurring reminder, and export their history to CSV.
- All financial calculations have tests.
- No part of the MVP touches the Stellar network.
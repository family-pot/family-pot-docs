# Glossary

**Claimable balance** — A Stellar ledger entry created by a sender that names a specific
claimant account and a predicate (e.g. a time window). The named claimant can later claim the
funds if the predicate is satisfied. Cannot be claimed by just anyone with a link.

**Predicate** — The condition attached to a claimable balance that determines when it can be
claimed (e.g. "before time X," "after time Y," "unconditional," or combinations). Evaluated
against ledger close time at the moment of the claim attempt, not at preview time.

**Trustline** — An explicit opt-in a Stellar account must create before it can hold a given
non-native asset (e.g. a stablecoin). Without a trustline, a claim or payment of that asset
fails.

**Reserve** — The minimum XLM balance a Stellar account must maintain. Creating a claimable
balance raises the creator's reserve requirement per claimant named.

**Horizon** — Stellar's RPC/REST API layer used to read ledger data and submit transactions.
Family Pot only uses it read-only until unsigned-transaction building is added in M4/M5.

**Corridor** — A specific sending-country-to-receiving-country pair (e.g. UK to Nigeria), used
when discussing fees, rates, and off-ramp availability for that pair.

**Off-ramp / anchor** — A service that converts a Stellar-network asset (e.g. a stablecoin) into
local fiat currency the recipient can actually use. Availability and cost vary by corridor and
are not guaranteed.

**Provenance (data)** — The origin/trust level of a displayed value: `user-entered`,
`calculated`, `estimated`, or `verified`. See `ARCHITECTURE.md`.

**Drips Wave** — The funding program this project is preparing for, which pays contributors by
issue complexity (Trivial 100 / Medium 150 / High 200 points) within a fixed time window per
wave.
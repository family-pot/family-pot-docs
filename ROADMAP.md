# Roadmap

Milestones: **M0** Foundation · **M1** Tracking MVP · **M2** Analytics and comparison ·
**M3** Recurring and export · **M4** Stellar verification · **M5** Claimable balance (experimental)

Complexity (Drips Wave points): **T** Trivial (100) · **M** Medium (150) · **H** High (200)

Each row names the repo the issue lives in. Cross-repo features are listed as two linked rows.

| ID | Issue | Repo | Cx | Milestone | Depends on |
| --- | --- | --- | --- | --- | --- |
| F1 | Scaffold, tooling, CI | web, api | — | M0 | none |
| F2 | Money utilities: minor units, decimal rates, rounding, tests | api | M | M0 | F1 (api) |
| F3 | Database schema and migrations | api | M | M0 | F1 (api) |
| T1a | Recipient model and API | api | M | M1 | F3 |
| T1b | Recipient UI (create, edit, delete) | web | M | M1 | T1a |
| T3a | Transfer model, validation, provenance field | api | M | M1 | F2, T1a |
| T3b | Transfer entry form | web | M | M1 | T3a |
| T5a | Transfer history endpoint with filters | api | M | M1 | T3a |
| T5b | Transfer history UI with filters | web | M | M1 | T5a |
| T6 | Edit and delete transfer with confirmation | web | T | M1 | T3b |
| A1 | Summary calculation endpoints | api | M | M2 | F2, T3a |
| A2 | Dashboard summary cards | web | T | M2 | A1 |
| A3a | Monthly totals aggregation endpoint | api | M | M2 | A1 |
| A3b | Monthly totals chart | web | M | M2 | A3a |
| A4 | Effective-cost analysis endpoint | api | M | M2 | A1 |
| A5 | Cumulative sent chart | web | T | M2 | A3b |
| C1 | Cost comparison engine with documented assumptions | api | H | M2 | F2, T3a |
| C2 | Comparison UI: actual vs estimated | web | M | M2 | C1 |
| C3 | Document comparison assumptions | docs | T | M2 | C1 |
| R1a | Recurring transfer model and API | api | M | M3 | T1a |
| R1b | Recurring transfer UI | web | M | M3 | R1a |
| R2 | Next-due date calculation | api | M | M3 | R1a |
| R3a | Due reminders endpoint | api | M | M3 | R2 |
| R3b | Due reminders UI, mark as sent | web | M | M3 | R3a, T3b |
| R4 | Email reminders | api | H | M3 | R2 |
| E1a | CSV export endpoint | api | M | M3 | T5a |
| E1b | CSV export UI trigger | web | T | M3 | E1a |
| S1 | Research ADR: claimable balance design and corridor | docs | M | M4 | none |
| S2 | Read-only Horizon client | api | M | M4 | F1 (api) |
| S3 | Verify a Stellar tx hash, mark transfer verified | api | H | M4 | S2, T3a |
| S4 | Full threat model update | docs | M | M4 | S1 |
| S5 | Build unsigned claimable-balance tx with sender reclaim | api | H | M5 | S1, S4 |
| S6 | Claim-status tracker | api | M | M5 | S5, S2 |
| S7 | Recipient claim page (no keys) | web | H | M5 | S5 |

## Cross-repo issue convention

When one feature needs work in two repos, open two issues, each stating:

> Related to [#N in family-pot-\<other-repo\>](link)

Neither issue closes until both are merged and verified working together.
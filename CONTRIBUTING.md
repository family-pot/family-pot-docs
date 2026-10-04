# Contributing to Family Pot

Family Pot is split across four repositories:

- [family-pot-web](https://github.com/family-pot/family-pot-web) — Next.js frontend
- [family-pot-api](https://github.com/family-pot/family-pot-api) — NestJS backend (REST)
- [family-pot-contracts](https://github.com/family-pot/family-pot-contracts) — reserved, inactive
- [family-pot-docs](https://github.com/family-pot/family-pot-docs) — this repo

This file is the shared contribution standard referenced by all four. Each repo's own
`CONTRIBUTING.md` covers only its local setup and points back here for everything else.

## Which repo does my issue belong to?

- Changes to UI, pages, client-side behavior → `family-pot-web`
- Changes to API endpoints, database, business logic, Stellar calls → `family-pot-api`
- Changes to product definition, architecture, roadmap, ADRs, threat model, or any doc listed
  in this repo's README → `family-pot-docs`
- Smart contract work → `family-pot-contracts`, and only after the ADR described there is
  accepted

A feature that touches both frontend and backend is **two linked issues**, one per repo, each
referencing the other with "Depends on" / "Related to #<issue> in <repo>". Do not mix frontend
and backend code in a single PR across repo boundaries — each PR stays inside one repo.

## Picking up work

1. Browse open issues in the relevant repo. Each has a `complexity:` label and a dependency list.
2. Only take issues whose dependencies are closed, in whichever repo those dependencies live.
3. If the issue is part of a Drips Wave, apply through Drips Wave and wait for assignment —
   one contributor per issue.
4. Ask questions on the issue before starting if anything is unclear.

Complexity levels (Drips Wave points): **Trivial** 100, **Medium** 150, **High** 200. If an
issue turns out to be bigger than labelled, say so on the issue before continuing rather than
after opening the PR.

## Branches, commits, PRs

- Branch naming: `feat/<issue>-short-name`, `fix/<issue>-short-name`, `docs/<issue>-short-name`
- Commits: [Conventional Commits](https://www.conventionalcommits.org/), e.g.
  `feat(tracking): add recipient model`
- One issue per PR, in the repo that issue belongs to. Reference it with `Closes #<number>`.
- Fill in the PR template fully. CI must be green before review.

## Rules for financial code (family-pot-api, and any money display in family-pot-web)

- **Never use floating point for money or exchange rates.** Use the shared money/decimal
  utilities, not raw JavaScript `number` arithmetic.
- **Every financial calculation needs tests**, including zero amounts, rounding, and large
  values.
- **Do not invent data.** No default or placeholder exchange rates, fees, or savings figures.
- **Respect data provenance.** Every number shown to a user is exactly one of: `user-entered`,
  `calculated`, `estimated`, or `verified` (confirmed on the Stellar network). Estimates must be
  visibly labelled, and their assumptions documented in `ASSUMPTIONS.md` in this repo.
- **Never handle Stellar secret keys.** No input fields, storage, logging, or URLs containing a
  secret key, in any repo. Signing happens in the user's own wallet.

## Documentation changes

- Doc-only issues and PRs happen in `family-pot-docs`.
- If a PR in `family-pot-web` or `family-pot-api` changes behavior that a shared doc describes
  (architecture, roadmap, assumptions, threat model), open a linked docs issue/PR here rather
  than editing local copies — this repo is the single source of truth.

## Code of conduct

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).
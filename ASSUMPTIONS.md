# Assumptions for estimates

Any calculation with provenance `estimated` must be documented here **before** it ships, by the
PR that implements it.

## Template

### <Calculation name>

- **Repo / issue:**
- **Purpose:**
- **Inputs (and their provenance):**
- **Formula:**
- **Rounding:**
- **What it deliberately ignores:** (e.g. rate movement between quote and settlement,
  recipient-side off-ramp costs, taxes, anchor fees)
- **Known limitations:**
- **Review date:** (assumptions about rates/fees should be periodically re-checked)

## Entries

_None yet. The first entry is added by issue C1 (cost comparison engine) in `family-pot-api`._
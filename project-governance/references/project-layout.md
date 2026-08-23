# Project layout

Use `.project/` at the repository root as the canonical governance directory.

## Required structure

```text
.project/
├── architecture-decisions/
├── sparks/
├── requirements/
├── policy-exceptions/
└── technical-debt/
```

Keep the complete directory under version control. Treat its contents as
project-local state belonging to the affected repository.

Use these fixed directory names. Do not relocate governed artefacts outside
`.project/`.

## Initialization

- Resolve the repository root before reading or changing governance state.
- When `.project/` does not exist, create the complete required structure.
- Create the governance directories without speculative work items.
- When an empty directory must be retained by Git, add a minimal `.gitkeep`.
- When `.project/` already exists, validate the required structure instead of
  recreating it.
- Report missing or invalid required content instead of silently replacing it.

## Governance usability

Treat the canonical governance store as usable when all of the following are
true:

- the required directory for the requested record type exists;
- the target directory can be determined unambiguously from the fixed project
  layout;
- existing records can be parsed and identified reliably enough to allocate an
  identifier and reconcile duplicates;
- creating or updating a record will not lose, overwrite, or duplicate
  governance state.

A violation of an individual governance rule does not by itself make the
governance implementation unusable. Filename discrepancies, stale status
suffixes, incomplete content, or another isolated record-level violation remain
governance violations, but use the canonical store when records can still be
stored and reconciled safely.

Use a fallback store only when the canonical store is absent or unusable. Do
not use fallback storage merely because governance is partially non-compliant.

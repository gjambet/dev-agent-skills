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

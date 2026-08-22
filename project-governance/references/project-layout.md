# Project layout

Use `.project/` at the repository root as the canonical governance directory.

## Required structure

```text
.project/
├── governance.yaml
├── sparks/
├── requirements/
└── technical-debt/
```

Keep the complete directory under version control. Treat its contents as project-local state belonging to the affected repository.

## Initialization

- Resolve the repository root before reading or changing governance state.
- When `.project/` does not exist, create the complete structure.
- Generate `.project/governance.yaml` with:

```yaml
version: 1

paths:
  sparks: sparks
  requirements: requirements
  technical_debt: technical-debt
```

- Create the configured work-item directories without speculative work items.
- When an empty directory must be retained by Git, add a minimal `.gitkeep`.
- When `.project/` already exists, validate it instead of recreating it.
- Report missing or invalid required content instead of silently replacing it.

## Path safety

Interpret paths in `.project/governance.yaml` relative to `.project/`. Reject absolute paths and paths that escape the governance root.

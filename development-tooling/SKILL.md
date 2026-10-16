---
name: development-tooling
description: Apply shared development-tooling and repository-management standards. Use when configuring Git repositories, dependencies between repositories, local development environments, build tooling, or project bootstrap workflows.
---

# Development Tooling

## Repository composition

- Never use Git submodules.
- Prefer independently versioned repositories with explicit installation, checkout, packaging, or dependency-management workflows.
- Do not introduce a submodule as a shortcut for sharing source code, configuration, documentation, skills, or build logic.
- When replacing an existing submodule, preserve reproducibility by documenting how the external content is obtained and which version is expected.
- Preserve stricter project-specific rules defined in the consuming repository's `AGENTS.md`.

## Backlog tooling

- Use GitHub tools for issue discovery, creation and lifecycle updates; use Workbench for registered repository edits and Git operations.
- Use GitHub Issues as the initiative and technical-debt source of truth. Do not bootstrap .project/sparks/, SPARKS/, docs/sparks/, .project/technical-debt/, root debt files or empty placeholders.
- Preserve requirements, policy exceptions, ADRs and designs in their existing local stores.

---
name: developer-tooling
description: Apply shared developer-tooling and repository-management standards. Use when configuring Git repositories, dependencies between repositories, local development environments, build tooling, or project bootstrap workflows.
---

# Developer Tooling

## Repository composition

- Never use Git submodules.
- Prefer independently versioned repositories with explicit installation, checkout, packaging, or dependency-management workflows.
- Do not introduce a submodule as a shortcut for sharing source code, configuration, documentation, skills, or build logic.
- When replacing an existing submodule, preserve reproducibility by documenting how the external content is obtained and which version is expected.
- Preserve stricter project-specific rules defined in the consuming repository's `AGENTS.md`.

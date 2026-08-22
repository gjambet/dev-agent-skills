---
name: project-governance
description: Establish and maintain the project-local governance structure used to record sparks, requirements, technical debt, and architecture decision records. Use when initializing or validating project governance, discovering project work, capturing or promoting an idea, managing requirements, recording technical debt, managing architecture decisions, or updating work-item relationships and lifecycle states.
---

# Project Governance

Resolve the repository root before reading or changing governance state. Use `.project/` as the project-local source of truth and keep it under version control.

Never store a consuming project's governed records in this skills repository. Preserve stricter project-specific rules defined in `AGENTS.md`.

## Workflow

1. Read [project-layout.md](references/project-layout.md) before initializing or validating `.project/`.
2. Read the reference for every work-item type involved:
   - [sparks.md](references/work-item-sparks.md)
   - [requirements.md](references/work-item-requirements.md)
   - [technical-debt.md](references/work-item-debts.md)
3. Read [architecture-decision-records.md](references/architecture-decision-records.md) before creating, changing, superseding, or validating an ADR.
4. Read [work-items-relationships-rules.md](references/work-items-relationships-rules.md) before creating, changing, removing, or validating relationships or evidence links.
5. Validate existing governance state before modifying it.
6. Preserve stable identifiers, history, evidence, and relationship integrity.

## Shared identity rules

- Store each work item in one Markdown file under its configured directory.
- Name each file `<id>.md`.
- Use `spark-<sequence>`, `requirement-<sequence>`, or `debt-<sequence>`.
- Allocate sequences independently for each work-item type.
- Determine the next sequence from active and terminal items.
- Never reuse an identifier or rename a file when its title or status changes.
- Store the descriptive title in metadata.
- Use ISO 8601 dates.

## Architecture decision identity

- Store each ADR in one Markdown file under its configured directory.
- Name each file `adr-<sequence>.md`.
- Allocate ADR sequences independently from work-item sequences.
- Never reuse an ADR identifier or rename its file.

## Shared change rules

- Do not populate speculative work items during initialization.
- Update the `updated` date whenever a work item changes.
- Record material lifecycle and relationship changes in history.
- Do not silently replace invalid governance content.
- Do not mark work implemented, verified, remediated, or resolved without the evidence required by its type reference.

---
name: project-governance
description: Establish and maintain the project-local governance structure used to record sparks, requirements, technical debt, policy exceptions, architecture decision records, and technical designs. Use when initializing or validating project governance, discovering project work, capturing or promoting an idea, managing requirements, recording technical debt, reviewing policy exceptions, managing architecture decisions or technical designs, or updating governed-record relationships and lifecycle states.
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
3. Read [policy-exceptions.md](references/policy-exceptions.md) before creating, changing, matching, expiring, or validating a policy exception.
4. Read [architecture-decision-records.md](references/architecture-decision-records.md) before creating, changing, superseding, or validating an ADR.
5. Read [technical-designs.md](references/technical-designs.md) before creating, changing, superseding, or validating a technical design.
6. Read [work-items-relationships-rules.md](references/work-items-relationships-rules.md) before creating, changing, removing, or validating relationships or evidence links.
7. Validate existing governance state before modifying it.
8. Preserve stable identifiers, history, evidence, and relationship integrity.

## Shared identity and filename rules

- Store each governed record in one Markdown file under its required directory.
- Use `spark-<sequence>`, `requirement-<sequence>`, `debt-<sequence>`,
  `adr-<sequence>`, `design-<sequence>`, or `policy-exception-<sequence>` as the stable
  identifier.
- Name each file `<id>-<short-topic>-<status>.md`.
- Derive `<short-topic>` from two to four meaningful words that identify the
  subject. Use lowercase kebab-case.
- Use the record's exact lifecycle status as `<status>`.
- Rename the file whenever its title or status changes. Never change the stable
  identifier stored in frontmatter.
- Allocate sequences independently for each governed-record type.
- Determine the next sequence from every active and terminal record regardless
  of its topic or status.
- Never reuse an identifier.
- Store the full descriptive title in metadata.
- Use ISO 8601 dates.

## Shared change rules

- Do not populate speculative work items during initialization.
- Update the `updated` date whenever a governed record changes.
- Record material lifecycle and relationship changes in history.
- Do not silently replace invalid governance content.
- Do not mark work implemented, verified, remediated, or resolved without the evidence required by its type reference.

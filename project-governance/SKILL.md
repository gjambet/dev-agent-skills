---
name: project-governance
description: Establish and maintain the project-local governance structure used to record sparks, requirements, and technical debt. Use when initializing project governance, discovering project work, capturing or promoting an idea, managing requirements, recording technical debt, or updating governed work-item relationships and lifecycle states.
---

# Project Governance

## Governance root

- Resolve the repository root before reading or changing governance state.
- Use `.project/` at the repository root as the canonical governance directory.
- Keep `.project/` under version control.
- Treat its contents as project-local state belonging to the affected repository.
- Never store project work items in this skills repository.
- Preserve stricter project-specific governance rules defined in `AGENTS.md`.

The governance structure is:

```text
.project/
├── governance.yaml
├── sparks/
├── requirements/
└── technical-debt/
```

## Governance initialization

- When `.project/` does not exist, initialize the complete governance structure.
- Copy `assets/governance.yaml` to `.project/governance.yaml`.
- Create the configured `sparks/`, `requirements/`, and `technical-debt/` directories.
- Do not populate speculative work items during initialization.
- When `.project/` exists, do not initialize or recreate it.
- Validate the existing governance structure before using or modifying it.
- Report missing or invalid required content instead of silently replacing it.

Interpret paths in `.project/governance.yaml` relative to `.project/`. Reject
paths that escape the governance root.

## Work-item taxonomy

### Spark

A spark captures an idea that has not yet been accepted as required project
behaviour. It preserves intent, context, value, open questions, and links to
related work. A spark does not authorize implementation.

### Requirement

A requirement defines accepted product or system behaviour. It must be precise
enough to determine whether an implementation satisfies it.

### Technical debt

Technical debt describes a working implementation or development setup that
creates measurable maintenance, reliability, security, operational, or
evolution cost.

Do not classify missing required behaviour as technical debt. Record it as a
requirement or defect through the project's configured process.

## Work-item storage and identity

- Store each work item in one Markdown file under its configured directory.
- Name every work-item file `<id>.md`.
- Use `spark-<sequence>`, `requirement-<sequence>`, or `debt-<sequence>` as its stable identifier.
- Store the descriptive title only in the work-item metadata.
- Allocate sequences independently for each work-item type.
- Never reuse an identifier, including after an item is closed.
- Never rename the file when its title or status changes.
- Determine the next sequence from active and closed items.

Examples:

```text
spark-0001.md
requirement-0001.md
debt-0001.md
```

Begin every work item with:

```yaml
---
id: requirement-0001
title: Record transaction costs
status: proposed
created: 2026-08-22
updated: 2026-08-22
related: []
---
```

- Use ISO 8601 dates.
- Use stable work-item identifiers in `related`, not filenames or mutable URLs.

## Lifecycle

Use these spark states:

```text
proposed -> promoted | rejected | withdrawn
```

- Promote a spark by creating one or more requirements.
- Link the spark and resulting requirements in both directions.
- Preserve a promoted spark as decision history.
- Do not transform a spark file into a requirement.

Use these requirement states:

```text
proposed -> accepted -> implemented -> verified
proposed -> rejected
accepted | implemented | verified -> deprecated
```

Do not mark a requirement as verified without recording verification evidence.

Use these technical-debt states:

```text
identified -> accepted -> remediating -> resolved
identified -> rejected
identified | accepted -> exception
```

An exception must include its justification and review or expiry condition.
Resolving technical debt requires evidence that the debt no longer exists.

## Work-item content

- Preserve context, statement, impact, evidence, relationships, and history when relevant.
- Give requirements testable acceptance criteria.
- Give technical debt evidence, affected components, concrete impact, expected remediation outcome, and resolution criteria.
- Record material lifecycle transitions in the work-item history.

# Architecture decision records

An architecture decision record (ADR) captures an architecturally significant decision, its context, considered alternatives, consequences, and status. Use an ADR for decisions that materially constrain system structure, technology, integration, data, security, deployment, or operations.

Do not use an ADR as a substitute for a requirement, implementation plan, or technical-debt item.

An ADR explains **why** an architectural choice was made. Put detailed
instructions for **how** that choice is implemented in a technical design under
`.project/technical-design/`. Linking the records is optional and should be done
only when it adds useful traceability.

## Storage and identity

- Store each ADR in the configured architecture-decisions directory.
- Name the file `adr-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact ADR lifecycle status for `<status>`.
- Rename the file whenever its title or status changes; keep `id` unchanged.
- Allocate ADR sequences independently from work-item sequences.
- Determine the next sequence from ADRs in every lifecycle state.
- Never reuse an identifier.

Example filename:

```text
adr-0001-postgresql-storage-proposed.md
```

Begin every ADR with:

```yaml
---
id: adr-0001
title: Use PostgreSQL for persistent storage
status: proposed
created: 2026-08-22
updated: 2026-08-22
relationships:
  related: []
---
```

Use ISO 8601 dates. Use stable governed-record identifiers in `related`.

## Required content

Use these sections:

```markdown
# <title>

## Context

## Decision

## Alternatives considered

## Consequences

## History
```

- Describe the forces and constraints that require a decision.
- State the decision precisely.
- Record meaningful alternatives and why they were not selected.
- Record positive, negative, and operational consequences.
- Record material status and relationship changes in history.

## Lifecycle

```text
proposed -> accepted | rejected
accepted -> deprecated | superseded
```

- Treat an accepted ADR as immutable decision history.
- Correct spelling or formatting without changing the decision's meaning.
- Create a new ADR when replacing an accepted decision.
- When superseding an ADR, identify the replacement ADR in both records' history and link both records through `relationships.related`.
- Do not delete rejected, deprecated, or superseded ADRs.

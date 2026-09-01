# Technical designs

A technical design explains in detail how a solution, subsystem, integration,
or reusable architectural pattern is supposed to be implemented. Use it as the
authoritative implementation design for a solution or as a reusable pattern for
future implementations.

An architecture decision record explains why an architectural choice was made,
including its context, alternatives, and consequences. A technical design
explains how to realize that choice. Do not use a technical design to replace
the decision history in an ADR, and do not overload an ADR with detailed
implementation instructions. A technical design does not require an ADR.

## Storage and identity

- Keep the permanent `.project/technical-design/` directory under version
  control, even when it contains no technical designs.
- Store every technical design in that directory.
- Use `design-<sequence>` as the stable identifier.
- Name each file `design-<sequence>-<short-topic>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Rename the file when its title changes; never change its stable identifier.
- Allocate design sequences independently and never reuse an identifier.
- Do not assign a lifecycle or status to technical designs. Maintain them as
  living project documentation under version control.

Begin every technical design with:

```yaml
---
id: design-0001
title: Authenticate browser sessions with Keycloak
created: 2026-09-01
updated: 2026-09-01
relationships:
  related: []
---
```

## Required content

Use the sections that apply, while preserving enough detail for another
engineer or agent to implement the design consistently:

```markdown
# <title>

## Purpose and scope

## Design

## Interfaces and data flows

## Implementation rules

## Failure handling and operational considerations

## Security considerations

## Validation

## Related decisions

## History
```

- Define components, responsibilities, boundaries, interfaces, protocols, data
  models, and significant flows.
- State mandatory implementation rules separately from illustrative examples.
- Describe relevant failure modes, recovery, observability, security, migration,
  and operational behavior.
- Identify where and how the design may be reused as a pattern.
- Optionally link relevant ADRs and governed work items with stable identifiers
  when the relationship adds useful traceability.
- When an ADR is linked, keep decision rationale in the ADR and summarize only
  enough context to make the design understandable.
- Do not create an ADR solely to satisfy a technical-design relationship.

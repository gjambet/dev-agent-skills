# Technical designs

A technical design explains in detail how a solution, subsystem, integration,
or reusable architectural pattern is supposed to be implemented. Use it as the
authoritative implementation design for a solution or as a reusable pattern for
future implementations.

An architecture decision record explains why an architectural choice was made,
including its context, alternatives, and consequences. A technical design
explains how to realize that choice. Do not use a technical design to replace
the decision history in an ADR, and do not overload an ADR with detailed
implementation instructions.

## Storage and identity

- Keep the permanent `.project/technical-design/` directory under version
  control, even when it contains no technical designs.
- Store every technical design in that directory.
- Use `design-<sequence>` as the stable identifier.
- Name each file `design-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact lifecycle status for `<status>`.
- Rename the file when its title or status changes; never change its stable
  identifier.
- Allocate design sequences independently and never reuse an identifier.

Begin every technical design with:

```yaml
---
id: design-0001
title: Authenticate browser sessions with Keycloak
status: draft
created: 2026-09-01
updated: 2026-09-01
relationships:
  related:
    - adr-0001
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
- Link relevant ADRs and governed work items with stable identifiers.
- Keep decision rationale in the related ADR; summarize only enough context to
  make the design understandable.

## Lifecycle

```text
draft -> active | rejected
active -> deprecated | superseded
```

- An `active` design is the current implementation guidance.
- Update an active design when clarification does not materially change its
  architecture or compatibility expectations.
- Create a new design when a material replacement must coexist with the
  previous guidance or preserving migration history matters.
- When superseding a design, link the replacement in both records and record
  the transition in their history.
- Retain rejected, deprecated, and superseded designs as project history.

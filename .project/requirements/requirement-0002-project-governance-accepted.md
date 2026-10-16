---
id: requirement-0002
title: Define project governance
status: accepted
created: 2026-08-23
updated: 2026-10-16
relationships:
  related:
    - https://github.com/gjambet/dev-agent-skills/issues/7
  implemented-by: []
---

# Define project governance

## Context

Agents need a deterministic, project-local governance framework for discovering
and maintaining project artefacts. Reusable governance rules belong in the
project-governance skill; the governed artefacts themselves belong in the
affected project.

## Required behaviour

The project-governance skill must define:

- The canonical GitHub issue store for initiatives and technical debt, and project-local storage for other governed artefact types.
- The identity, filename, metadata, required content, and lifecycle of each
  artefact type.
- The rules for creating, updating, relating, and retaining governed artefacts.
- The relationships allowed between governed artefacts and implementation
  evidence.
- How agents initialize and validate the governance layout.
- How specialised skills discover and follow the governance framework without
  defining competing storage or lifecycle rules.

The governed artefacts must include:

- GitHub initiative issues (formerly sparks).
- Requirements.
- Technical-debt items.
- Policy exceptions.
- Architecture decision records.
- Technical designs.

## Storage rules

- Keep requirements, policy exceptions, ADRs and designs under the affected repository's `.project/` directory. Keep initiatives and technical debt in that repository's GitHub Issues.
- Keep technical designs in the permanent `.project/technical-design/`
  directory.
- Keep project governance state under version control.
- Keep reusable workflows and schemas in this skills repository.
- Never copy a consuming project's governed artefacts into this skills
  repository.
- Reject configured paths that escape the governance root.

## Content rules

For every governed artefact type, define:

- Stable identity and filename rules.
- Required frontmatter.
- Required body content.
- Lifecycle states and transition rules where the artefact uses a lifecycle.
- History and retention rules.
- Type-specific evidence requirements where applicable.
- A clear separation between ADRs that explain why an architectural decision
  was made and technical designs that explain in detail how the solution is to
  be implemented.
- Technical designs must not require lifecycle statuses or a related ADR.

## Relationship rules

- Use stable governed-record identifiers when relating governed artefacts.
- Define whether each relationship is reciprocal or directional.
- Preserve relationship integrity when records change.
- Report dangling, invalid, duplicate, or inconsistent relationships.
- Support links from requirements and technical debt to implementation
  artefacts where applicable.

## Acceptance criteria

- A validated `project-governance/SKILL.md` exists.
- The skill routes agents to focused reference files through progressive
  disclosure.
- Storage is defined for every governed artefact type.
- Expected metadata and content are defined for every governed artefact type.
- Lifecycle and retention rules are explicit where applicable.
- Relationship semantics and integrity rules are explicit.
- Every record has one owning repository; GitHub Issues is authoritative for initiatives and technical debt, while other governance stays project-local.


## Initiative backlog migration — 2026-10-16

GitHub Issues is now the canonical initiative backlog. Historical spark identifiers, paths and verification commands above describe the pre-migration state; they are not current filesystem requirements. Refer to:

- `spark-0001`: https://github.com/gjambet/dev-agent-skills/issues/7


## Backlog storage standard — 2026-10-16

Updated the accepted governance requirement to reflect the project owner's GitHub Issues standard for initiatives and technical debt. Source-controlled documents remain authoritative for requirements, exceptions, decisions and designs.

---
id: requirement-0002
title: Define project governance
status: accepted
created: 2026-08-23
updated: 2026-08-23
relationships:
  related:
    - spark-0001
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

- The canonical project-local storage location for each governed artefact type.
- The identity, filename, metadata, required content, and lifecycle of each
  artefact type.
- The rules for creating, updating, relating, and retaining governed artefacts.
- The relationships allowed between governed artefacts and implementation
  evidence.
- How agents initialize and validate the governance layout.
- How specialised skills discover and follow the governance framework without
  defining competing storage or lifecycle rules.

The governed artefacts must include:

- Sparks.
- Requirements.
- Technical-debt items.
- Policy exceptions.
- Architecture decision records.

## Storage rules

- Keep governed artefacts under the affected repository's `.project/`
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
- Lifecycle states and transition rules.
- History and retention rules.
- Type-specific evidence requirements where applicable.

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
- Lifecycle and retention rules are explicit.
- Relationship semantics and integrity rules are explicit.
- The framework remains project-local and independent of a specific issue
  provider.

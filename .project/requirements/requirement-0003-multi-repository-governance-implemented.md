---
id: requirement-0003
title: Support multi-repository application governance
status: implemented
created: 2026-09-17
updated: 2026-09-17
relationships:
  related: []
  originated-from: []
  implemented-by:
    - type: source
      reference: project-governance/SKILL.md
    - type: source
      reference: project-governance/references/application-topology.md
    - type: source
      reference: project-governance/references/project-layout.md
    - type: source
      reference: project-governance/references/work-items-relationships-rules.md
  verified-by: []
---

# Support multi-repository application governance

## Context

A logical application can be split across multiple repositories, for example a backend repository and a separate web application repository. Repository-local governance must remain independently usable while application-wide decisions and relationships need a deterministic coordination model.

## Required behaviour

The project-governance skill must support an optional `.project/application.md` topology record for multi-repository applications.

The topology must identify:

- A stable application identifier.
- The current repository and its role.
- Every participating repository and its role.
- Exactly one explicit master repository.

When no master is supplied during initialization, a single backend repository must be selected by default. If there is no unique backend repository, the master must be chosen explicitly.

Repository-specific governance remains local. Application-wide or cross-repository governance belongs to one canonical repository and defaults to the master repository unless another repository is the clear technical owner.

Cross-repository governed-record relationships must use stable qualified identifiers and must not require duplication of the governed item.

## Acceptance criteria

- Multi-repository applications have a defined `application.md` schema.
- Every application has exactly one explicit master repository.
- A unique backend repository is the default master during initialization.
- Every participating repository retains a complete local `.project/` governance structure.
- Application-wide governed items have one canonical owner and are not duplicated across repositories.
- Cross-repository relationships have a deterministic qualified-reference format.
- Agents do not load every participating repository for purely local work.

## Impact

This extends project governance discovery, layout validation, record ownership, and relationship validation for applications that span multiple repositories.

## History

- 2026-09-17: Requirement implemented with application topology, master-repository selection, ownership, discovery, and cross-repository relationship rules.

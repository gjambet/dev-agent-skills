# Project governance

## Intent

Create a reusable `project-governance` skill that gives agents a deterministic
way to discover, classify, relate, create, update, and close project work.

The skill defines the governance contract. It does not store the state of
individual projects.

## Responsibilities

- Define the canonical work-item taxonomy.
- Define the authoritative storage for each information type.
- Define identifiers, lifecycle states, required metadata, and deduplication.
- Define relationships between requirements, defects, implementation,
  technical debt, exceptions, and architectural decisions.
- Distinguish project-local truth from portfolio-level aggregation.
- Define how specialised skills discover and maintain existing work.

## Work-item taxonomy

- Requirement: required product or system behaviour.
- Defect: implementation that does not satisfy an accepted requirement.
- Technical debt: a working implementation that creates maintenance,
  reliability, or evolution cost.
- Compliance debt: technical debt demonstrated by divergence from an applicable
  engineering rule.
- Exception: intentional and justified non-compliance with an expiry or review
  condition.
- Decision: the rationale for an architectural or technical choice.

## Source-of-truth rules

- Store requirements, defects, and technical debt as work items in the affected
  project's configured provider.
- Store architectural decisions as versioned ADRs in the affected project.
- Store permanent exceptions as versioned project configuration linked to a
  work item or ADR.
- Store applicable skills and governance configuration in the affected project.
- Store only project references and aggregate reporting in a portfolio
  repository.
- Store reusable workflows, schemas, and templates in this skills repository.
- Never copy project work items into this skills repository.

## Project contract

Define a versioned project-local entry point, initially:

```text
.project/governance.yaml
```

The contract must support:

- stable project identity;
- provider and location for each work-item type;
- configured labels or equivalent classification;
- ADR location;
- applicable skills;
- exception location;
- optional portfolio registration.

Keep the schema provider-neutral while supplying a GitHub Issues example.

## Specialised processes

`project-governance` is foundational. Specialised skills such as
`project-compliance`, requirements management, security review, dependency
maintenance, and portfolio reporting must consume its contract rather than
inventing their own storage and lifecycle rules.

## Acceptance criteria

- A validated `project-governance/SKILL.md` exists.
- The work-item taxonomy and lifecycle are explicit.
- Authoritative storage is discoverable from project-local configuration.
- Deduplication and stable identity rules are defined.
- Relationships between work-item types are supported.
- GitHub Issues can be used without making the contract GitHub-specific.
- Project state remains in the affected project.
- Portfolio state contains references and aggregates only.

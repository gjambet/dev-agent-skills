# Technical debt

Technical debt describes a working implementation or development setup that creates measurable maintenance, reliability, security, operational, or evolution cost.

Do not classify missing required behaviour as technical debt. Record it as a requirement or defect through the project's configured process.

## Storage and identity

- Store each technical-debt item in the configured technical-debt directory.
- Name the file `debt-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact technical-debt lifecycle status for `<status>`.
- Rename the file whenever its title or status changes; keep `id` unchanged.
- Allocate sequences independently from other work-item types.
- Determine the next sequence from debt items in every lifecycle state.
- Never reuse an identifier.

Example filename:

```text
debt-0001-position-calculation-identified.md
```

Begin every technical-debt item with:

```yaml
---
id: debt-0001
title: Duplicate position calculation
status: identified
created: 2026-08-22
updated: 2026-08-22
relationships:
  related: []
  affects: []
  remediated-by: []
  verified-by: []
---
```

Use ISO 8601 dates. Order work-item identifiers lexicographically and keep them unique.

## Required content

Include evidence, affected components, concrete impact, expected remediation outcome, resolution criteria, relationships, and material history.

## Lifecycle

```text
identified -> accepted -> remediating -> resolved
identified -> rejected
```

- Record intentional justified divergence as a separate policy exception, not
  as a technical-debt lifecycle state.
- Move an item to `resolved` only when `remediated-by` identifies the remediation and `verified-by` proves that the debt no longer exists.
- Record every material lifecycle transition in its history.
- Apply [work-items-relationships-rules.md](work-items-relationships-rules.md) whenever relationships or evidence links change.

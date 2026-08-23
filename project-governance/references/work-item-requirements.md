# Requirements

A requirement defines accepted product or system behaviour. Make it precise enough to determine whether an implementation satisfies it.

## Storage and identity

- Store each requirement in the configured requirements directory.
- Name the file `requirement-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact requirement lifecycle status for `<status>`.
- Rename the file whenever its title or status changes; keep `id` unchanged.
- Allocate sequences independently from other work-item types.
- Determine the next sequence from requirements in every lifecycle state.
- Never reuse an identifier.

Example filename:

```text
requirement-0001-transaction-costs-proposed.md
```

Begin every requirement with:

```yaml
---
id: requirement-0001
title: Record transaction costs
status: proposed
created: 2026-08-22
updated: 2026-08-22
relationships:
  related: []
  originated-from: []
  implemented-by: []
  verified-by: []
---
```

Use ISO 8601 dates. Order work-item identifiers lexicographically and keep them unique.

## Required content

Include context, a precise behavioural statement, testable acceptance criteria, impact, relationships, and material history.

## Lifecycle

```text
proposed -> accepted -> implemented -> verified
proposed -> rejected
accepted | implemented | verified -> deprecated
```

- Move a requirement to `implemented` only when `implemented-by` contains valid implementation evidence.
- Move a requirement to `verified` only when `verified-by` contains valid verification evidence and the acceptance criteria have been checked.
- Preserve evidence and material lifecycle transitions in the requirement history.
- Apply [work-items-relationships-rules.md](work-items-relationships-rules.md) whenever relationships or evidence links change.

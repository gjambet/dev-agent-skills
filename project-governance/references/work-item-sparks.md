# Sparks

A spark carries an initiative from its initial capture through framing, implementation, and achievement. It preserves intent, context, expected value, constraints, relationships, and material history.

## Storage and identity

- Store each spark in the configured sparks directory.
- Name the file `spark-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact spark lifecycle status for `<status>`.
- Rename the file whenever its title or status changes; keep `id` unchanged.
- Allocate sequences independently from other work-item types.
- Determine the next sequence from sparks in every lifecycle state.
- Never reuse an identifier.

Example filename:

```text
spark-0001-transaction-costs-sparked.md
```

Begin every spark with:

```yaml
---
id: spark-0001
title: Record transaction costs
status: sparked
created: 2026-08-22
updated: 2026-08-22
relationships:
  related: []
---
```

Use ISO 8601 dates. Order identifiers lexicographically and keep them unique.

## Required content

Preserve the spark's intent, context, expected value, open questions, constraints, relationships, and material history.

As the spark advances:

- In `sparked`, capture the idea and why it may be valuable.
- In `framed`, define the intended outcome, scope, constraints, and sufficient requirements to guide implementation.
- In `in-implementation`, record the active implementation context and material progress.
- In `achieved`, record the delivered outcome.

## Lifecycle

```text
sparked -> framed -> in-implementation -> achieved
```

- Do not start implementation before the spark is `framed`.
- Preserve an `achieved` spark as project history.
- Do not reuse or repurpose an achieved spark for additional work.
- Record every material lifecycle transition in its history.

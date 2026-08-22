# Sparks

A spark captures an idea that has not yet been accepted as required project behaviour. It preserves intent, context, value, open questions, and links to related work. A spark does not authorize implementation.

## Storage and identity

- Store each spark in the configured sparks directory.
- Name the file `spark-<sequence>.md`.
- Allocate sequences independently from other work-item types.
- Never reuse an identifier or rename its file.

Begin every spark with:

```yaml
---
id: spark-0001
title: Record transaction costs
status: proposed
created: 2026-08-22
updated: 2026-08-22
relationships:
  related: []
  promoted-to: []
---
```

Use ISO 8601 dates. Order identifiers lexicographically and keep them unique.

## Required content

Preserve the spark's intent, context, expected value, open questions, constraints, relationships, and material history.

## Lifecycle

```text
proposed -> promoted | rejected | withdrawn
```

- Promote a spark only by creating one or more requirements.
- Link the spark and resulting requirements according to [work-items-relationships-rules.md](work-items-relationships-rules.md).
- Preserve a promoted spark as decision history.
- Do not transform, rename, or move a spark into a requirement.
- Record every material lifecycle transition in its history.

# Policy exceptions

A policy exception records an intentional, justified, and bounded divergence
from an applicable skill rule. Use it only when compliance is currently
inappropriate or impractical for a defined scope.

Do not use a policy exception to hide an accidental violation, avoid
remediation indefinitely, or weaken a rule for an entire project without a
specific justification.

## Storage and identity

- Store each policy exception in the configured policy-exceptions directory.
- Name the file `policy-exception-<sequence>-<short-topic>-<status>.md`.
- Use two to four meaningful lowercase kebab-case words for `<short-topic>`.
- Use the exact policy-exception lifecycle status for `<status>`.
- Rename the file whenever its title or status changes; keep `id` unchanged.
- Allocate sequences independently from other governed-record types.
- Determine the next sequence from exceptions in every lifecycle state.
- Never reuse an identifier.

Example filename:

```text
policy-exception-0001-legacy-package-name-active.md
```

Begin every policy exception with:

```yaml
---
id: policy-exception-0001
title: Retain legacy package name during migration
status: active
created: 2026-08-23
updated: 2026-08-23
policy:
  skill: java-coding-standards
  rule: Package naming
scope:
  - src/main/java/com/example/legacy
review:
  on: 2026-11-23
relationships:
  related: []
---
```

Use the skill name and a stable, unambiguous rule heading or rule identifier.
Define scope narrowly enough to determine whether a finding is covered.

## Required content

Use these sections:

```markdown
# <title>

## Justification

## Consequences

## Review condition

## History
```

- Explain why compliance is intentionally deferred or inappropriate.
- Describe the risks and operational consequences of the exception.
- Define a dated review or explicit expiry condition.
- Record material status, scope, justification, and review changes in history.

## Lifecycle

```text
proposed -> active -> expired | revoked
proposed -> rejected
```

- Treat only an `active` exception as applicable.
- Activate an exception only when its skill, rule, scope, justification, risks,
  and review or expiry condition are complete.
- Treat an exception as expired when its expiry date or review condition has
  elapsed without explicit renewal.
- Reassess the exception whenever its skill rule, affected scope, or project
  context changes.

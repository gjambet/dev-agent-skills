---
name: java-coding-standards
description: Apply reusable Java coding and class-design standards. Use when creating, modifying, or reviewing Java classes, refactoring responsibilities, or deciding whether a type should be nested or top-level.
---

# Java Coding Standards

## Class design

- Prefer top-level classes with one clearly defined responsibility.
- Do not introduce nested or inner classes when the type has an independent responsibility.
- Extract such types into dedicated top-level classes.
- Allow a small implementation-local type only when it has no meaningful responsibility or use outside its enclosing class.
- Preserve stricter project-specific rules defined in the consuming repository's `AGENTS.md`.

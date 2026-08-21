---
name: java-coding-standards
description: Apply reusable Java coding and class-design standards. Use when creating, modifying, or reviewing Java classes, refactoring responsibilities, deciding whether a type should be nested or top-level, or choosing between static and instance methods.
---

# Java Coding Standards

## Class design

- Prefer top-level classes with one clearly defined responsibility.
- Do not introduce nested or inner classes when the type has an independent responsibility.
- Extract such types into dedicated top-level classes.
- Allow a small implementation-local type only when it has no meaningful responsibility or use outside its enclosing class.

## Static methods and state

- Prefer instance methods for application, domain and infrastructure behaviour.
- Do not use mutable static state for application services or business data.
- Allow private static methods for naturally stateless implementation details, including pure functions, trivial conversions and private factories.
- Keep static methods private whenever possible.
- When reusable behaviour requires a public API, extract it into a dedicated class and expose it through an instance method.
- Allow public static methods only when required by Java or a framework.
- Do not create general-purpose public static utility classes.

## Project overrides

- Preserve stricter project-specific rules defined in the consuming repository's `AGENTS.md`.

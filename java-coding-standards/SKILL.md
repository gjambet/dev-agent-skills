---
name: java-coding-standards
description: Apply reusable Java coding and class-design standards. Use when creating, modifying, or reviewing Java classes, packages, refactoring responsibilities, deciding whether a type should be nested or top-level, or choosing between static and instance methods.
---

# Java Coding Standards

## Java version

- Java projects must target the latest generally available Long-Term Support (LTS) Java release.
- Apply the selected LTS version consistently across build configuration, compiler/release settings, Maven or Gradle toolchains and enforcers, CI runtimes, container base images, and documented local-development requirements.
- Do not leave a project on an older LTS solely because it currently builds successfully there. Treat an older Java LTS as a compliance issue to remediate unless a documented project constraint prevents the upgrade.
- When the latest LTS changes, new work and compliance reviews must use the new LTS as the target; do not hard-code a particular Java version into this reusable rule.
- If a dependency, runtime platform, deployment environment, or other concrete constraint prevents use of the latest LTS, document the exception through the project's policy-exception process rather than silently lowering the Java version.

## Package naming

- Use lowercase snake_case for every Java package segment.
- Separate words in a multiword segment with underscores.
- Do not use uppercase letters, camelCase, PascalCase or hyphens in package names.
- Use `me.guillaume.order_management`, not `me.guillaume.orderManagement`, `me.guillaume.OrderManagement` or `me.guillaume.order-management`.
- Apply this rule when creating or renaming packages; do not perform unrelated legacy package migrations.
- When a package migration is in scope, update package declarations, imports, source-directory paths, tests and relevant build or framework configuration consistently.

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

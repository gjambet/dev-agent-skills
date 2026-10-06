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

## Server-side template page models

- For server-side rendered templates such as Thymeleaf, use a dedicated typed page/view model for each template rather than assembling the template contract from unrelated `Model` attributes in controllers.
- Every concrete page template must have exactly one dedicated immutable page/view model. **Each page/view model must have its own dedicated factory class: the mapping is strictly 1 model = 1 factory. A factory must never construct or return a different page model, and a shared/multi-model factory is forbidden.** Reusable fragments may define their own typed fragment models when they have a non-trivial data contract; the same 1:1 factory rule applies when a fragment model requires a factory.
- Controllers must not assemble template state with unrelated `Model` attributes. A route rendering a page obtains the page model from its factory and exposes that single page contract to the template.
- The factory is the completeness boundary for rendering. All mandatory template state must be constructor/record components of the page model and must be supplied by the factory, so missing mandatory state cannot survive compilation or factory construction and fail later during template rendering.
- Mandatory page-model components must also be enforced at runtime by the page model itself. For reference values, use compact record constructors or equivalent immutable-constructor validation with `Objects.requireNonNull(...)`; defensively copy mandatory collections with `List.copyOf(...)`, `Set.copyOf(...)`, `Map.copyOf(...)`, or the appropriate immutable equivalent. Apply domain validation for mandatory scalar values where their valid range is narrower than the Java type. A factory returning a page model with invalid or missing mandatory state must therefore fail immediately at construction time, never later during Thymeleaf rendering.
- Do not weaken mandatory state into nullable fields, optional model attributes, empty placeholder values, or defensive template null checks merely to support inconsistent controller paths. Model genuinely optional UI state explicitly (`Optional`, sealed variants, dedicated nullable semantics where justified). Decide mandatory versus optional from the template contract: if rendering assumes a value exists, that value is mandatory.
- Centralize defaults, derived presentation data, breadcrumbs, labels, collections and other template-facing composition in the page-model factory. Keep HTTP routing, request parsing, authorization and redirect decisions in controllers.
- A template must read its functional state through its dedicated page model rather than depending on a bag of unrelated root variables. Cross-cutting framework/infrastructure attributes that are independent of the page contract may remain global.
- **Every page-model factory requires its own unit test.** The factory test must exercise each supported creation path/variant and verify the complete model contract: every mandatory component is populated with the expected value, derived/default presentation values are correct, collections are complete, and genuinely optional state has the expected semantics. Where the factory depends on services/repositories, isolate it with test doubles and verify the composition logic rather than duplicating controller tests.
- Factory tests must include relevant failure/boundary cases for mandatory state. At minimum, page-model constructor validation must make it impossible for a factory regression to silently return a model with missing mandatory state.
- Tests for every route rendering a template must verify that the dedicated factory-backed page model is provided. Add architecture/compliance tests where practical to prevent controllers from reintroducing arbitrary page `Model` assembly and to ensure every page model has exactly one dedicated factory and every page-model factory has a corresponding unit test.

## Project overrides

- Preserve stricter project-specific rules defined in the consuming repository's `AGENTS.md`.

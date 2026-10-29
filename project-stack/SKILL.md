---
name: project-stack
description: Apply the required project technology stack. Use when creating, bootstrapping, modifying, or reviewing Java projects, choosing build tools, application frameworks, or database schema migration tools, or auditing stack compliance.
---

# Project Stack

## Java projects

- Use Maven as the build and dependency-management tool for every Java project.
- Define the build in `pom.xml`; use a root Maven reactor for multi-module projects.
- Use Spring Boot as the application framework for Java projects.
- Keep local development, CI, and container builds aligned with the Maven build and Spring Boot configuration.
- Do not introduce Gradle, Ant, or an alternative application framework as a substitute for this required stack.

## Backend database schemas

- Use Flyway for versioned schema migrations in every backend that manages a relational database schema.
- Store migrations in version control and apply them through Flyway as part of application startup or the deployment workflow.
- Use Flyway as the schema evolution mechanism; do not rely on Hibernate automatic schema creation or updates in production.
- Set Hibernate `ddl-auto` to `validate` or `none` when Hibernate is used.
- Add new migrations for subsequent changes; do not modify migrations already applied to shared environments.
- Do not require Flyway for backends that manage no relational database schema.

## Existing projects

- Check the build configuration and application bootstrap when assessing compliance; a declared dependency alone does not prove that the required stack is used.
- Report existing deviations through the `project-compliance` workflow and its policy-exception and technical-debt rules.
- Keep any migration scoped to the requested work; do not silently rewrite an existing project's stack.

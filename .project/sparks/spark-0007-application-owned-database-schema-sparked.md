---
id: spark-0007
title: Keep application database schema in the application
status: sparked
created: 2026-09-13
updated: 2026-09-13
relationships:
  related: []
---

# Keep application database schema in the application

## Intent

Define a reusable engineering rule that keeps application database structure with the application that owns it rather than embedding application table DDL in hosting-infrastructure repositories.

## Expected outcome

Hosting infrastructure is responsible for provisioning the database boundary required to run an application, including the database/schema namespace, ownership, credentials, connectivity, and privileges. The application repository is responsible for creating and evolving the tables, indexes, constraints, and other application-owned database objects inside that provisioned boundary.

Application-owned DDL should therefore be versioned, tested, and deployed with the application, using an application-controlled initialization or migration mechanism. Infrastructure code must not become the source of truth for application tables.

## Expected value

This keeps the database model coupled to the code that consumes it, avoids cross-repository deployment ordering for ordinary schema changes, and gives each application explicit ownership of its persistence model while preserving infrastructure ownership of database provisioning and access control.

## Constraints

- Infrastructure may create the database or schema namespace and grant the application the privileges needed within it.
- Infrastructure must not define application tables, indexes, application-level constraints, or routine table migrations.
- Application schema changes must remain safe for existing deployed databases and use an idempotent initializer or explicit migration mechanism as appropriate.
- Shared platform-owned database objects remain infrastructure concerns when they are genuinely not owned by a single application.

## Open questions

- Should the eventual rule require a migration framework once an application exceeds simple idempotent initialization?
- What threshold should distinguish a platform-owned database object from an application-owned object?

## History

- 2026-09-13: Captured after moving Dev Workbench MCP `execution_log` table DDL out of `host.oups.net` and into the application repository.

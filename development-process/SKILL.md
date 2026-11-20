---
name: development-process
description: Apply the shared feature-branch workflow, issue tracking, and delivery gates. Use when implementing, validating, committing, merging, or pushing changes. Apply the Maven pre-push gate in Maven-based projects.
---

# Development Process

## Feature branches

- Always implement changes on a dedicated feature branch.
- For issue-based work, include the issue number and a short descriptive slug in the branch name, for example `feature/46-task-prerequisites`.
- After confirming a feature branch has merged into the default branch, delete it locally and on the remote. Apply this rule after every merge, including a partial implementation of an issue.
- For the next increment of the same issue, create a fresh branch from the updated default branch. Keep the original issue-based name and add an incrementing numeric suffix, for example `feature/46-task-prerequisites-2`, then `feature/46-task-prerequisites-3`.

## Maven pre-push gate

- Always run the complete Maven test suite immediately before every push.
- Run the tests from the repository root so the complete Maven reactor is covered.
- Use the repository-specific full-test command when it is defined in `AGENTS.md`; otherwise run `mvn test`.
- Do not treat targeted module tests as a substitute for the complete pre-push test suite.
- Do not push when any test fails.
- If the complete test suite cannot be executed, stop before pushing and report the blocker explicitly.
- After any code or test change made following the test run, run the complete Maven test suite again before pushing.

## Initiative and technical-debt tracking

- Use the owning repository's GitHub Issues for ideas, initiatives and technical debt. Read project-governance/references/github-issues.md before backlog discovery, capture or migration.
- Search existing open and closed issues, keep progress and evidence on the issue, and reference its URL in delivery work.
- Never create or maintain spark/debt Markdown records or obsolete backlog directories in repositories.

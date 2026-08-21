---
name: development-process
description: Apply shared development workflow and delivery gates. Use when implementing, validating, committing, or pushing changes in Maven-based projects, especially before publishing commits to a remote repository.
---

# Development Process

## Maven pre-push gate

- Always run the complete Maven test suite immediately before every push.
- Run the tests from the repository root so the complete Maven reactor is covered.
- Use the repository-specific full-test command when it is defined in `AGENTS.md`; otherwise run `mvn test`.
- Do not treat targeted module tests as a substitute for the complete pre-push test suite.
- Do not push when any test fails.
- If the complete test suite cannot be executed, stop before pushing and report the blocker explicitly.
- After any code or test change made following the test run, run the complete Maven test suite again before pushing.

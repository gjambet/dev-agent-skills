---
id: spark-0002
title: Project compliance
status: sparked
created: 2026-08-21
updated: 2026-08-23
relationships:
  related:
    - spark-0001
  promoted-to: []
---

# Project compliance

## Intent

Create a reusable `project-compliance` skill that detects divergence between a
project and its declared engineering skills, then maintains the corresponding
technical-debt backlog through the `project-governance` contract.

## Dependency

`project-compliance` depends on `project-governance`. It must not define a
separate work-item taxonomy, lifecycle, or storage model.

## Responsibilities

- Discover the skills applicable to a project.
- Compare the implementation and development setup with those skills.
- Classify findings as regressions, existing debt, or intentional exceptions.
- Create, update, deduplicate, and close compliance-debt work items.
- Preserve evidence, first detection, last confirmation, severity, scope, and
  acceptance criteria.
- Prevent new objective violations in changed code.
- Recommend opportunistic remediation only when it is directly related and low
  risk.

## Check triggers

- Perform a full baseline when a project adopts compliance management.
- Reconcile the full repository when applicable skills change materially.
- Inspect changed code and its direct dependencies during ordinary development.
- Perform scheduled full reconciliation for active projects.
- Review critical findings and expired exceptions before a major release.
- Revalidate a finding before starting its remediation.

## Enforcement

- Use deterministic tools and CI for objectively enforceable rules.
- Use agent review for rules requiring engineering judgment.
- Block regressions detected by objective checks.
- Do not block unrelated delivery because of baselined existing debt.
- Do not perform unsolicited repository-wide remediation.

## Backlog reconciliation

Identify a finding by:

```text
repository + skill + rule + affected component
```

During reconciliation:

- confirm whether every open finding still exists;
- close resolved findings;
- update changed scope and evidence;
- merge duplicates;
- create newly detected findings;
- do not recreate a resolved item unless the violation reappears.

## Acceptance criteria

- A validated `project-compliance/SKILL.md` exists.
- The skill explicitly requires and follows `project-governance`.
- Initial, incremental, scheduled, and release-oriented checks are defined.
- Regression, existing debt, and exception handling are unambiguous.
- Compliance debt is stored in the affected project, never in this skills
  repository.
- The skill can reconcile an existing backlog without creating duplicate work
  items.

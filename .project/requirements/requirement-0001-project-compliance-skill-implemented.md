---
id: requirement-0001
title: Define project compliance skill behaviour
status: implemented
created: 2026-08-23
updated: 2026-09-01
relationships:
  related:
    - spark-0002
  implemented-by:
    - type: source
      reference: project-compliance/SKILL.md
---

# Define project compliance skill behaviour

## Context

The project-compliance skill operationalizes the project-compliance spark. It
must use the project-governance framework rather than defining a separate
taxonomy, lifecycle, or storage model.

## Required behaviour

The project-compliance skill must:

- Discover the engineering skills and framework applicable to a project.
- Compare the implementation and development setup with those rules.
- Determine whether each divergence is unjustified debt or an intentional
  exception with adequate justification.
- Classify findings as regressions, existing debt, or intentional exceptions.
- Create, update, deduplicate, and close compliance-debt work items.
- Preserve evidence, first detection, last confirmation, severity, scope, and
  acceptance criteria.
- Prevent new objective violations in changed code.
- Recommend opportunistic remediation only when directly related and low risk.
- Treat every skill present in this repository as applicable to the consuming
  project, including skills added in the future.
- Discover applicable skills dynamically instead of maintaining a fixed list.
- Require project documentation to be written in English and require an English
  glossary under `.project/` when specific business needs require retaining
  foreign-language terminology.
- Check for a valid matching policy exception before recording a violation as
  technical debt.
- Store compliance debt in the project-governance technical-debt directory when
  governance is valid.
- Store compliance debt in the repository root when project-governance is
  absent or incorrectly implemented.

## Check triggers

The skill must:

- Perform a full baseline when a project adopts compliance management.
- Reconcile the full repository when applicable skills change materially.
- Inspect changed code and its direct dependencies during ordinary development.
- Support scheduled full reconciliation for active projects.
- Review critical findings and expired exceptions before a major release.
- Revalidate a finding before starting remediation.

## Enforcement

The skill must:

- Use deterministic tools and CI for objectively enforceable rules.
- Use agent review for rules requiring engineering judgment.
- Block regressions detected by objective checks.
- Not block unrelated delivery because of baselined existing debt.
- Not perform unsolicited repository-wide remediation.

## Backlog reconciliation

Identify a finding by:

```text
repository + skill + rule + affected component
```

During reconciliation, the skill must:

- Confirm whether every open finding still exists.
- Close resolved findings.
- Update changed scope and evidence.
- Merge duplicates.
- Create newly detected findings.
- Not recreate a resolved item unless the violation reappears.

## Acceptance criteria

- A validated `project-compliance/SKILL.md` exists.
- The skill explicitly requires and follows `project-governance`.
- Initial, incremental, scheduled, and release-oriented checks are defined.
- Regression, existing debt, and justified-exception handling are unambiguous.
- Compliance debt is stored in the affected project, never in this skills
  repository.
- All current and future skills in this repository are discovered automatically.
- Invalid or missing governance cannot prevent a compliance violation from
  being recorded.
- The skill reconciles an existing backlog without creating duplicate work
  items.

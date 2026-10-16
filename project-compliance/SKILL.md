---
name: project-compliance
description: Check whether a project complies with every engineering skill in this skills repository, including skills added later, and reconcile violations with valid policy exceptions or technical-debt issues. Use when baselining, reviewing, auditing, changing, releasing, or periodically reconciling a project's compliance with its engineering framework.
---

# Project Compliance

Require the project to comply with every skill present in this skills
repository. Discover the applicable skill set on every compliance run; never
maintain a fixed list.

## Applicable skills

1. Resolve the repository that contains this `project-compliance` skill.
2. Recursively discover every `SKILL.md` representing a skill in that repository.
3. Treat every discovered skill as applicable, including `project-compliance`
   and skills added after this skill was written.
4. Read each applicable `SKILL.md` and every reference it requires for the
   rules being checked.
5. Apply stricter project-specific rules from the consuming project's
   `AGENTS.md` in addition to repository skills.

Do not treat examples, assets, generated files, or nested reference documents
as independent skills.

## Documentation language

- Write project documentation in English.
- Use a non-English word or expression only when a specific business need
  requires the original term and an English replacement would lose relevant
  meaning.
- When project documentation contains such a term, create or update
  `.project/glossary.md` and define the term there in English. Include its
  source language, business meaning, and the reason the original term is
  retained.
- Keep the glossary under version control and update it in the same change that
  introduces, changes, or removes the documented term.
- Do not require glossary entries for source-code identifiers, registered names,
  third-party product names, or verbatim quotations that are not part of the
  project's own explanatory prose.

Treat undocumented foreign-language business terminology and project
documentation written in a language other than English as compliance
violations. Do not create an empty glossary when no qualifying term is used.

## Compliance workflow

For every applicable rule:

1. Identify the concrete project scope governed by the rule.
2. Inspect the project with deterministic tools when the rule is objectively
   testable; use engineering review when judgment is required.
3. Classify a divergence as a compliance violation.
4. Search for a matching policy exception.
5. If a valid matching exception exists, record the finding as excepted and do
   not create technical debt.
6. Otherwise create or update one technical-debt issue for the violation.
7. Reconcile existing records by updating evidence and scope, merging
   duplicates, and resolving records whose violations no longer exist.

Identify the same finding across runs by:

```text
skill + rule + affected component
```

Do not create a new record merely because the evidence or wording changed.

## Policy exceptions

When the canonical policy-exception store defined by `project-governance` is
usable, read its policy-exception rules and search `.project/policy-exceptions/`.
A violation elsewhere in the governance layout does not prevent this search.

Treat an exception as valid only when:

- it identifies the applicable skill and rule;
- its scope covers the affected component;
- its status is active;
- its justification explains why non-compliance is intentional;
- its review or expiry condition has not elapsed;
- all required metadata and content satisfy `project-governance`.

An absent, malformed, inactive, expired, unrelated, or insufficiently justified
exception does not suppress a violation. Record the reason the candidate
exception was rejected in the debt evidence.

## Debt storage

Use GitHub Issues in the owning repository as the sole technical-debt store, regardless of whether local .project/ governance exists. Read project-governance/references/work-item-debts.md and github-issues.md before capture or migration.

- Search open and closed issues by skill, rule and affected component; update or reopen the existing matching finding.
- Include concrete evidence, impact, remediation and verification criteria, and relevant exception or requirement links.
- Do not create .project/technical-debt/, root debt-*.md files, legacy debt stores or their placeholders.
- Treat missing or invalid local governance as a separate finding where applicable, without requiring a local debt store to report it.
- When GitHub is unavailable, report the blocker and retain unmigrated source records. Do not claim complete reconciliation or silently create a second backlog.

## Check triggers

- Perform a full baseline when a project adopts compliance management.
- Reconcile the full repository whenever the skills repository changes.
- Inspect changed code, configuration, documentation, tests, and direct
  dependencies during ordinary development.
- Perform scheduled full reconciliation for active projects.
- Review critical findings and expired exceptions before a major release.
- Revalidate a finding before starting its remediation.

## Enforcement

- Use deterministic tooling and CI for objectively enforceable rules.
- Use agent review for rules requiring engineering judgment.
- Block new objective violations in changed scope.
- Do not block unrelated delivery because of baselined existing debt.
- Do not perform unsolicited repository-wide remediation.
- Do not create an exception to make a compliance check pass.

## Reconciliation

During every reconciliation:

- confirm whether each open compliance-debt record still represents a violation;
- update last-confirmed evidence and affected scope;
- resolve records whose violations no longer exist;
- reopen or create a record when a resolved violation reappears;
- merge duplicates without losing history;
- re-evaluate every matching exception for status, scope, review, and expiry;
- report invalid governance separately from the violations it prevents the
  framework from storing normally.

Return a summary containing the applicable skills, checked rules, compliant findings, exceptions, GitHub debt issues, unresolved access failures and evidence.

## GitHub initiative and debt backlogs

- Read project-governance/references/github-issues.md and validate the initiative and debt backlogs against that standard.
- Reject new or remaining tracked spark records, local debt records and obsolete backlog-directory placeholders, including legacy locations.
- Confirm migrated records have corresponding issues with preserved content, lifecycle, history and working inbound links before accepting source removal.
- Treat an unavailable GitHub connection as incomplete backlog validation, not proof that no initiatives exist.
- Apply the unchanged local rules to requirements, policy exceptions, ADRs and designs.

---
name: project-compliance
description: Check whether a project complies with every engineering skill in this skills repository, including skills added later, and reconcile violations with valid policy exceptions or technical-debt records. Use when baselining, reviewing, auditing, changing, releasing, or periodically reconciling a project's compliance with its engineering framework.
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
6. Otherwise create or update one technical-debt record for the violation.
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

Use `.project/technical-debt/` whenever the canonical technical-debt store is
usable according to `project-governance`, even when one or more governance
rules are violated.

A filename discrepancy, stale status suffix, incomplete record, or other
isolated governance violation makes the affected record non-compliant; it does
not make the entire governance implementation unusable. Record or update the
finding in the canonical technical-debt directory and report the governance
violation separately.

Treat the canonical technical-debt store as unusable only when safe
reconciliation is not possible, including when:

- `.project/technical-debt/` is missing;
- the required target directory cannot be determined unambiguously;
- existing records cannot be reliably parsed or identified;
- writing there could lose, overwrite, or duplicate governance state.

When the canonical technical-debt store is absent or unusable:

- store or update the finding in the repository root;
- use `debt-<sequence>-<short-topic>-<status>.md` and the technical-debt
  format defined by the imported `project-governance` skill when it can be
  read;
- otherwise preserve at minimum a stable identifier, title, status, dates,
  violated skill, violated rule, affected component, evidence, impact, and
  remediation criteria;
- record the missing or unusable governance store as a separate compliance
  violation;
- migrate or merge root debt records into `.project/technical-debt/` after
  the canonical store becomes usable.

Never discard a root debt record during migration. Preserve its identifier when
available and avoid creating a duplicate governed record.

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

Return a summary containing the applicable skills, checked rules, compliant

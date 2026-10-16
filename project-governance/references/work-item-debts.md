# Technical debt in GitHub Issues

Technical debt describes an existing implementation or development setup that creates measurable maintenance, reliability, security, operational or evolution cost. Missing required behavior belongs in a requirement or defect, not automatically in technical debt.

## Canonical store and identity

- Store technical debt in GitHub Issues in the owning repository. Follow [github-issues.md](github-issues.md) for migration, ownership, remote verification and duplicate handling.
- Do not create or retain .project/technical-debt/, root debt-*.md records, legacy debt directories or empty placeholders.
- Use the issue URL or owner/repository#number as the canonical identity. Preserve old debt identifiers only as migration metadata and historical references.
- Distinguish debt using the title prefix [Tech Debt] and an existing appropriate label when available; optional label availability must not block capture.

## Required content

Record the affected component, observed evidence, concrete impact, expected remediation, resolution criteria, relationships and material history. For compliance findings, include the violated skill and rule and reconcile by skill + rule + affected component.

- Search open and closed issues before creating a new finding.
- Link requirements, relevant policy exceptions and immutable implementation or verification evidence.
- Preserve original created/updated dates and lifecycle history in migrated content.
- Preserve complete source content and commit-pinned source links before removing a legacy record.
- Update retained governance relationships to canonical issue URLs, and link related governed documents from the issue.

## Lifecycle

Keep identified, accepted and remediating debt open, with progress recorded in the issue body, comments or optional project fields. Close as completed only when remediation evidence and verification demonstrate that the debt no longer exists. Close as not planned only when explicitly rejected or intentionally abandoned.

During migration, preserve an existing resolved state as closed/completed, and rejected as closed/not planned, without claiming new validation. Do not resolve unrelated open debt merely because this migration changes its storage location.

Keep policy exceptions as separate local governed records. An exception may suppress a matching compliance finding only when it is valid, active and in scope; it is not a debt lifecycle state.

## Reconciliation

- Revalidate findings before remediation and on later compliance runs.
- Update evidence on the existing issue when the same violation persists.
- Reopen a prior issue when the same resolved violation returns.
- Merge duplicates with cross-links and preserved history.
- If issue access is unavailable, report incomplete reconciliation and retain any unmigrated source. Do not fall back to root Markdown debt files or claim that the backlog is empty.

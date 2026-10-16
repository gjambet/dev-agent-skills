# GitHub issue backlog

Use GitHub Issues as the canonical store for initiatives, ideas formerly called sparks, and technical debt. Apply this rule to every consuming repository and to this skills repository itself.

## Ownership and identity

- Create an issue in the owning GitHub repository. For application-wide work, follow application-topology.md and prefer the declared master repository unless another repository is the clear technical owner.
- Search open and closed issues before creating one. Update an existing matching issue rather than duplicating it.
- Identify an issue by its canonical HTTPS URL or owner/repository#number. Do not allocate new spark or debt identifiers.
- Do not create or retain spark records, SPARKS/, docs/sparks/, .project/sparks/, empty spark-directory placeholders, local debt records, .project/technical-debt/ or a parallel Markdown backlog.
- Keep requirements, policy exceptions, ADRs and technical designs in their existing governed stores. Apply work-item-debts.md for debt-specific classification, evidence and closure rules.

## Content and lifecycle

- Capture intent, context, expected value, scope, constraints, open questions and testable acceptance criteria when known.
- Link relevant requirements, designs, decisions, implementation and verification evidence.
- Keep discussion and material progress in issue updates or comments.
- Use open issues for pending or active work. Close as completed only with delivery evidence; use not planned for explicitly abandoned work.
- Preserve historical lifecycle values when migrating records. An existing achieved or resolved record maps to a closed completed issue without asserting new validation.
- Use labels or project fields for finer workflow states only when available; do not make issue creation depend on optional labels.
- Frame scope and acceptance criteria before implementation. Do not reuse a completed issue for unrelated additional work.

## Migration

1. Inventory current tracked records and their owning repositories; include legacy locations and terminal records.
2. Check existing open and closed issues for the legacy identifier, source path and matching intent.
3. Create or update exactly one issue per initiative or debt record. Preserve the complete original content, metadata, history, evidence, lifecycle and stable legacy identifier.
4. Include a source permalink pinned to the original commit. Preserve old evidence as historical evidence, not as a newly executed check.
5. Resolve legacy relationships to issue URLs, and link retained governed documents from the issue.
6. Confirm the issue body and open/closed state before deleting its source record. If GitHub is unavailable, retain the source and report the blocker; never silently lose backlog data.
7. Update live inbound relationships and remove obsolete spark and debt directory placeholders. Keep a compact legacy-ID-to-issue mapping when needed to resolve historical references; it must not become a second editable backlog.
8. Validate links and counts, review the diff, run required checks, and publish through the normal repository workflow.

## Discovery and validation

- Read the repository's GitHub issue backlog when discovering initiative work; the absence of local spark files does not mean the backlog is empty.
- Treat new or remaining tracked spark or debt records/directories as a compliance violation.
- Report unavailable issue access as incomplete validation, not as an empty backlog.
- Keep migration idempotent and preserve source content until confirmed remote storage exists.

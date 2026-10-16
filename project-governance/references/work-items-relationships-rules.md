# Work-item relationship rules

Use typed relationships to preserve traceability between GitHub initiative and debt issues, requirements, policy exceptions, architecture decisions, technical designs, implementation, and verification evidence.

## Representation

For local governed records, store relationships in frontmatter. For GitHub initiative and debt issues, record relationships in the issue body or comments with canonical links. Local representation:

```yaml
relationships:
  related: []
```

Use stable governed-record identifiers for relationships between work items,
architecture decision records, and technical designs. Do not use filenames,
paths, titles, or mutable document URLs as governed-record identifiers. For GitHub initiatives and technical debt, use the canonical issue HTTPS URL as the external identity in related or originated-from; verify the issue exists. Preserve legacy spark and debt IDs only in migration mappings and historical text.

For a relationship to a governed record owned by another repository in the same multi-repository application, qualify the stable identifier with the repository identifier from `.project/application.md`:

```yaml
relationships:
  related:
    - gjambet/quittances-api:requirement-0012
```

Use bare identifiers for local records owned by the current repository. Use qualified identifiers only for cross-repository local-record references. Issue URLs are valid for same-repository and cross-repository initiative and debt relationships.

Use evidence entries for links to implementation or verification artifacts:

```yaml
relationships:
  implemented-by:
    - type: source
      reference: src/main/java/com/example/Trade.java
    - type: pull-request
      reference: https://github.com/example/project/pull/42
```

Keep entries unique and deterministic. Order work-item identifiers lexicographically.

## Governed-record relationships

### `related`

- Use `related` for a meaningful relationship that has no more specific type.
- Record it in both governed records.
- Add and remove both sides in the same change. For an issue-to-document relationship, link the governed document from the issue and the canonical issue URL from the document; preserve reciprocal intent without copying the backlog into Git.

### `affects`

- Record affected requirements on the debt issue with their repository paths or stable IDs and links.
- Add the canonical debt issue URL to the affected requirement's `related` list unless a more specific reverse relationship is defined.
- Do not use `affects` as a substitute for documenting affected components and concrete impact.

### Architecture decisions and technical designs

- An ADR-to-technical-design relationship is optional.
- When such a relationship adds useful traceability, link the ADR and technical
  design through `related` in both records.
- Do not require or create an ADR merely because a technical design exists.
- Do not duplicate decision rationale in the technical design or detailed
  implementation instructions in the ADR.
- A technical design may relate to multiple ADRs, and an ADR may be realized by
  multiple technical designs.

## Evidence relationships

Evidence relationships are directional. They do not require modification of the referenced artifact.

### `implemented-by`

- Use `implemented-by` on requirements.
- Reference verifiable implementation artifacts such as source files, commits, or pull requests.
- Require at least one valid entry before changing a requirement to `implemented`.
- Preserve entries as implementation history.

### `remediated-by`

- Record remediation evidence on technical-debt GitHub issues.
- Reference the source changes, commits, or pull requests that remove the debt.
- Do not treat remediation evidence alone as proof of resolution.

## Integrity

When adding or changing a relationship:

- Verify that every referenced governed-record identifier exists, and verify each GitHub issue URL remotely when issue access is available. Report unavailable remote verification explicitly.
- For a qualified cross-repository reference, verify that the repository is listed in `.project/application.md` and verify the target record in that repository when it is accessible.
- Reject self-references and duplicate entries.
- Update the `updated` date of every modified work item.
- Record material relationship changes in history.

For reciprocal cross-repository relationships, update both owning repositories as one coordinated change. If one repository is unavailable, do not claim relationship integrity is fully validated; report the incomplete reciprocal update explicitly.

When validating governance state:

- Report dangling identifiers, missing reciprocal work-item relationships, self-references, duplicates, and invalid evidence entries.
- Do not silently repair invalid relationships unless the task explicitly authorizes modification.
- Keep relationships to terminal records; closed, rejected, withdrawn, deprecated, verified, and resolved items remain valid relationship targets.

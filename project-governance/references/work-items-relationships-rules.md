# Work-item relationship rules

Use typed relationships to preserve traceability between sparks, requirements, technical debt, policy exceptions, architecture decisions, technical designs, implementation, and verification evidence.

## Representation

Store relationships in the work-item frontmatter:

```yaml
relationships:
  related: []
```

Use stable governed-record identifiers for relationships between work items,
architecture decision records, and technical designs. Do not use filenames,
paths, titles, or mutable URLs as governed-record identifiers.

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
- Add and remove both sides in the same change.

### `affects`

- Use `affects` from technical debt to each requirement whose implementation or verification is affected.
- Add the debt item to the affected requirement's `related` list unless a more specific reverse relationship is defined.
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

- Use `remediated-by` on technical-debt items.
- Reference the source changes, commits, or pull requests that remove the debt.
- Do not treat remediation evidence alone as proof of resolution.

## Integrity

When adding or changing a relationship:

- Verify that every referenced governed-record identifier exists.
- Reject self-references and duplicate entries.
- Update the `updated` date of every modified work item.
- Record material relationship changes in history.

When validating governance state:

- Report dangling identifiers, missing reciprocal work-item relationships, self-references, duplicates, and invalid evidence entries.
- Do not silently repair invalid relationships unless the task explicitly authorizes modification.
- Keep relationships to terminal records; closed, rejected, withdrawn, deprecated, verified, and resolved items remain valid relationship targets.

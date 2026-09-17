# Application topology

Use `.project/application.md` when one logical application spans more than one repository.

The file identifies the application, the local repository's role, the participating repositories, and the single master repository used for application-level governance coordination. It does not replace the repository-local `.project/` governance store.

## Required representation

Use Markdown with YAML frontmatter:

```yaml
---
application-id: quittances
repository: gjambet/quittances-api
repository-role: backend
master-repository: gjambet/quittances-api
repositories:
  - repository: gjambet/quittances-api
    role: backend
  - repository: gjambet/quittances-web
    role: webapp
---

# Application topology
```

Rules:

- `application-id` is a stable identifier shared by every repository in the application.
- `repository` identifies the repository containing this copy of `application.md`.
- `repository-role` describes the local repository's role. Use a concise lowercase kebab-case value such as `backend`, `webapp`, `mobile-app`, or `worker`.
- `master-repository` identifies exactly one repository listed under `repositories`.
- `repositories` lists every repository currently participating in the application and its role.
- Repository identifiers must be stable repository names such as `owner/repository`, not mutable web URLs.

Every participating repository should contain an `application.md`. The `application-id`, `master-repository`, and `repositories` values must agree across copies. The `repository` and `repository-role` fields are local to each repository.

The master repository's application topology is authoritative when copies disagree. Report drift; do not silently rewrite a member repository's topology.

## Selecting the master repository

Always persist the master explicitly in `master-repository`; do not rely on implicit inference after initialization.

When initializing a multi-repository application and no master is specified:

- If exactly one participating repository has role `backend`, select it as the master repository.
- If there is no backend repository, or more than one backend repository, require an explicit master selection.

Changing the master repository is an application-topology change. Update every participating repository's `application.md` as one coordinated change and report any repository that could not be updated.

## Governance ownership

Each repository keeps a complete local `.project/` structure and remains authoritative for governance items it owns.

- Keep repository-specific work in the repository it affects.
- Give each governed item exactly one owning repository.
- Store application-wide or cross-repository governance items in the master repository by default unless another repository is the clear technical owner.
- Do not duplicate the same governed item in multiple repositories.
- Reference governed items owned by another repository instead of copying them.

The master repository coordinates application-level governance; it does not become the storage location for all repository-local work.

## Discovery behaviour

When an agent works in a repository that has `application.md`:

- Read the local topology first.
- Keep a purely local task scoped to the current repository.
- Consult the master repository or another member repository only when the task is application-scoped, depends on cross-repository governance, or changes application topology.
- Do not load every member repository merely because they belong to the same application.

If a referenced member repository is unavailable, state that cross-repository validation is incomplete rather than guessing its governance state.

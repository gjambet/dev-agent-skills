# Dev Agent Skills

Reusable development skills shared across projects.

Each skill lives in its own directory and contains a required `SKILL.md`. A skill may keep detailed rules in directly linked `references/` files so agents load only the material needed for the current task.

```text
dev-agent-skills/
├── java-coding-standards/
│   └── SKILL.md
├── development-tooling/
│   └── SKILL.md
├── development-process/
│   └── SKILL.md
├── project-governance/
│   ├── SKILL.md
│   └── references/
│       ├── project-layout.md
│       ├── architecture-decision-records.md
│       ├── technical-designs.md
│       ├── policy-exceptions.md
│       ├── work-item-sparks.md
│       ├── work-item-requirements.md
│       ├── work-item-debts.md
│       └── work-items-relationships-rules.md
└── project-compliance/
    └── SKILL.md
```

The `project-governance` skill defines project-local storage, work-item lifecycles, policy exceptions, architecture decision records, technical designs, and typed traceability relationships. ADRs explain why an architectural choice was made; technical designs under `.project/technical-design/` explain how it is implemented. Requirements use `implemented-by` to reference verifiable implementation artifacts.

The `project-compliance` skill checks every skill present in this repository, including future skills, and reconciles unjustified violations into the affected project's technical-debt records. It also requires project documentation to be written in English and places definitions for business-required foreign-language terms in `.project/glossary.md`.

Projects consume this repository through their `.agents/skills` directory. Keep project-specific configuration in the consuming project's `AGENTS.md`; keep reusable workflows and standards here.

Governed records use readable filenames in the form `<id>-<short-topic>-<status>.md` while retaining a stable identifier in frontmatter.

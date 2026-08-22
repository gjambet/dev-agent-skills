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
└── project-governance/
    ├── SKILL.md
    └── references/
        ├── project-layout.md
        ├── sparks.md
        ├── requirements.md
        ├── technical-debt.md
        └── work-items-relationships-rules.md
```

The `project-governance` skill defines project-local storage, work-item lifecycles, and typed traceability relationships. Requirements use `implemented-by` to reference verifiable implementation artifacts and `verified-by` to record verification evidence.

Projects consume this repository through their `.agents/skills` directory. Keep project-specific configuration in the consuming project's `AGENTS.md`; keep reusable workflows and standards here.

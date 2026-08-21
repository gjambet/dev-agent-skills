# Dev Agent Skills

Reusable development skills shared across projects.

Each skill lives in its own directory and contains a required `SKILL.md`:

```text
dev-agent-skills/
├── pmo-project-process/
│   └── SKILL.md
├── java-project-engineering/
│   └── SKILL.md
└── delivery-quality-gates/
    └── SKILL.md
```

Projects consume this repository through their `.agents/skills` directory. Keep project-specific configuration in the consuming project's `AGENTS.md`; keep reusable workflows and standards here.

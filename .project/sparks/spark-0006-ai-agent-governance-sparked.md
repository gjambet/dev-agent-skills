---
id: spark-0006
title: Introduce AI agent governance
status: sparked
created: 2026-09-03
updated: 2026-09-03
relationships:
  related:
    - spark-0001
---

# Introduce AI agent governance

Projects need explicit governance for work performed with AI agents so that durable project knowledge resides in the repository rather than depending on conversation history or agent memory.

The governance should define the repository as the source of truth for project state, decisions, requirements, work items, implementation context, and other durable knowledge. Conversations should be treated as transient working context, with material outcomes persisted into governed project artefacts before they are relied upon by later work.

The governance should also define how agents recover project context, record material changes, hand work between conversations or agents, and avoid creating undocumented project knowledge that exists only in a chat session.

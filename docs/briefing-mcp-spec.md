# Briefing MCP — precomputed cross-domain briefing specification

Status: proposal; not implemented. Date: 2026-10-15.

## Purpose
Provide fast, evidence-backed, prioritized headlines to a conversational assistant (provisional name: Freya). Collect and analyze information *before* the user asks. This MCP is generic and not limited to software operations.

## Scope (iteration 1)
- Reactive consumption of precomputed daily and incremental briefings; no autonomous remediation.
- Sources: ProdObserver/Loki, GitHub CI/deployments, application events (including registrations and alerts), optionally connected email and calendar, and later Home Assistant.
- User asks for headlines first, then drills into a specific item and its evidence.
- Data gathering must not delay the initial response; return the most recent snapshot with freshness metadata.

## Architecture
1. Independent source collectors run on schedules, with timeouts, retries, least-privilege credentials, and per-source health/freshness tracking.
2. Normalize observations and deduplicate recurring incidents/events with stable fingerprints.
3. Prioritize by severity, novelty, relevance, and actionability. Summarize into concise headlines with source references; never fabricate missing evidence.
4. Persist in PostgreSQL, independent of the voice or chat interface.
5. Expose read-oriented MCP tools for the assistant.

Suggested storage:
- briefing_runs(id, started_at, finished_at, status, source_statuses)
- briefing_items(id, fingerprint, category, priority, headline, summary, first_seen_at, last_seen_at, state, evidence_refs)
- briefing_snapshots(id, generated_at, coverage_window, freshness, headline_item_ids, summary)

Store references and selective excerpts rather than unnecessary raw copies of sensitive source data. Define retention and access controls.

## MCP tool candidates
- get_latest_briefing(scope?, max_items?) -> headline list, generated_at, per-source freshness, partial-failure flags.
- get_briefing_item(item_id) -> explanation, chronology, references, current status.
- list_briefing_items(filters?) -> query by category, priority, novelty, state and time.
- acknowledge_item(item_id) -> optional future controlled write operation, not required for iteration 1.

## Scheduling and performance
- Configurable collection cadences per source (illustrative: operational events every 15 minutes; mail/calendar hourly).
- Generate a daily snapshot before expected morning use, plus incremental refreshes.
- Serve cached headlines in seconds without waiting for upstream calls.
- Clearly mark stale or unavailable sources and retain last known valid snapshot.

## Security and operations
- Isolate source credentials; per-user authorization and data partitioning, particularly for email/calendar.
- Treat collected content as untrusted; defend against prompt injection.
- Audit collection, synthesis, retrieval and future actions. Avoid logging secrets or private message bodies.
- Containerized service integrated with existing Docker/PostgreSQL stack; independent lifecycle from Browser MCP and read-only ProdObserver.
- Monitor job failures, lag, duplicate rate, and response latency.

## Acceptance criteria
- A morning briefing can be retrieved without live fan-out to sources.
- Every headline links to evidence or is explicitly marked as an inference.
- Duplicate recurring incidents do not reappear as new headlines.
- Partial source outages are visible and do not block retrieval.
- Drill-down supports investigating a headline with underlying references.
- No autonomous corrective actions in iteration 1.

## Evolution
Iteration 2 may introduce proactive notifications, user feedback/acknowledgment, priority learning, and tightly scoped approved actions. Keep assistant branding (Freya, provisional) configurable and separate from MCP service names.

Related: docs/browser-mcp-e2e-testing-spec.md.

---
name: improve-project
description: Run a multi-area project audit, record evidence-backed opportunities, and start a separate implementation session for safe, reversible improvements. Use for «Улучшай проект» and broad project-improvement requests.
---

# Improve Project

Use this skill as the shared workflow for Codex Desktop, Codex CLI, and OpenCode. The current chat is the audit orchestrator. Implementation runs in a fresh session using a handoff file.

At the start of each run, read the relevant section of `references/runtime-adapters.md` to choose the active runtime’s agent IDs and fresh-session mechanism.

## Audit phase

1. Confirm the project root and read applicable `AGENTS.md` files. Inspect `git status --short --branch` before reading or changing anything. Preserve all existing edits and untracked files. Never read secrets or bulk media as source code.
2. Read the prior `.improve/PROJECT-MAP.md` and recent `.improve/runs/` reports when present. On the first run, map the repository comprehensively. On later normal runs, inspect changed tracked and untracked source, relevant callers/dependencies, and prior open findings. Rebuild the full map when project structure or stack changes materially. A request for a deep/full audit forces full coverage.
3. Inspect project briefs, current product/design documentation, tests, build/config files, and relevant runtime surfaces. Treat prior audit findings as history and verify whether they remain open before repeating them.
4. Ask independent agents to inspect product fit, generate product ideas, review UX/design, audit engineering, and examine quality/reliability in parallel. Add the project mapper on the first run and whenever the map is stale. Give each agent a precise area, read-only source boundary, and the shared output contract in `references/audit-protocol.md`. Agents return findings to the orchestrator; the orchestrator writes all run files to avoid concurrent report edits.
5. The orchestrator checks every proposed finding against the cited evidence, removes duplicates, distinguishes observed facts from inferences and hypotheses, ranks by user impact, confidence, effort, and risk, and records rejected or deferred ideas with a short reason.
6. Save the project map and the run under `.improve/`. Follow `references/handoff.md`. Keep the map useful and compact; do not copy the repository into it.

For substantial product, UX, design-system, or architecture proposals, load the relevant Hackathon OS guidance and research proportionally. External evidence that can change a recommendation needs a direct source URL and date checked; prefer primary sources and label facts separately from inference. A small bug or narrow cleanup does not need a market study.

## Automatic implementation boundary

After the audit, automatically send only findings that are evidence-backed, high-confidence, bounded, reversible, and preserve documented user-visible behavior. Each task needs a clear result and acceptance criteria.

Hold for the user’s choice any proposal that removes or adds a user-visible feature, changes a material workflow or product rule, migrates or deletes user data, changes a public/API contract, introduces a paid/external service, or depends on an unresolved product decision. Feature brainstorming produces candidates; it does not authorize those changes.

## Fresh implementation session

When the run has auto-eligible tasks, start a separate, clean session with the implementation handoff. The new session’s primary agent is the implementation orchestrator; it launches the matching `developer-*` agents and integrates their work. Keep the audit chat read-only apart from reports and handoff files.

- **Codex Desktop:** use the connected Codex app task/thread tool when available, selecting the same local project and checkout. Start it with the run’s `handoff.md` path and a prompt to implement only its auto-eligible tasks, verify each task is still current, and use the matching `developer_*` agents. Do not rerun the audit.
- **Codex CLI:** start a new `codex exec` task from the repository root with the handoff path in its prompt. Do not resume the audit transcript.
- **OpenCode:** start a new `opencode run --agent project-improver` session from the repository root with the handoff path in its prompt. Do not continue the audit session.
- If the current runtime cannot create a new session, leave the complete handoff in `.improve/`, report that automatic session creation was unavailable, and provide the exact prompt to start it manually. Never claim that a new chat started unless the runtime confirms it.

The implementation orchestrator reads the handoff, rechecks current Git state and task freshness, and assigns one matching developer agent per task (`developer_product`, `developer_designer`, `developer_engineering`, or `developer_quality` in Codex; hyphenated equivalents in OpenCode). Implement independent non-overlapping work in parallel; serialize tasks that may touch the same files or shared interfaces. Each developer stays within its assigned scope and reports changed files, checks actually run, and remaining uncertainty. The orchestrator reviews the combined diff against each finding and updates run status. Do not commit, push, publish, or deploy.

## Invocation and modes

- “Улучшай проект” runs the normal delta-aware cycle.
- “Улучшай проект глубоко” or “полный аудит” forces a comprehensive audit.
- If there is no map, normal mode starts with the comprehensive pass.
- If there are no auto-eligible findings, save the report and stop without creating an empty implementation session.
- On OpenCode, `/improve-project` starts the audit. Afterward, start the implementation in a separate `opencode run` session using the handoff command from `references/runtime-adapters.md`. On Codex, invoke `$improve-project`; if the desktop connector cannot create the implementation chat, use a new Desktop chat or a fresh `codex exec` run with the saved handoff.

Read [audit protocol](references/audit-protocol.md) for agent scope and finding criteria and [handoff format](references/handoff.md) for stored artifacts.

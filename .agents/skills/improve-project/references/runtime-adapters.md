# Runtime adapters

The workflow and report contracts stay shared. Only agent registration and new-session launch differ.

## Codex Desktop and CLI

- Store project-scoped custom agent profiles in `.codex/agents/` as TOML. The current chat is the audit orchestrator; a separate new session is the implementation orchestrator.
- Use `project_mapper` when the map is missing/stale, then `product_auditor`, `idea_generator`, `design_auditor`, `engineering_auditor`, and `quality_auditor` for applicable audit scopes. Implementation agents are prefixed `developer_`.
- In Desktop, create a fresh chat/task under the same project and checkout when the connected Codex app tooling supports it. Pass the handoff path and use the same working-tree state so the ignored `.improve/` files and current user changes remain visible. Prompt it to implement only the handoff’s auto-eligible tasks, recheck freshness, and use the matching `developer_*` agents; do not rerun the audit. If the connector is unavailable, leave this as a ready-to-paste prompt for a new chat; never implement inside the audit chat.
- In CLI, run a new command from the repository root, for example: `codex exec "Read .improve/runs/<run-id>/handoff.md and implement only the auto-eligible tasks in it."` Do not use resume/fork for the implementation phase; the handoff is the carried context.
- Codex subagents inherit the parent session’s sandbox and approval settings. Their prompts require read-only source exploration during audit, but this is not an OS-level write lock; the orchestrator compares Git state before and after. If an auditor changes source files, preserve those changes, mark the affected tasks blocked, and ask the user how to proceed. Never reset or discard work automatically.

## OpenCode

- OpenCode discovers the shared skill under `.agents/skills/`. Register project agents as Markdown files in `.opencode/agents/`; the orchestrator is primary and specialists are subagents.
- Use `project-mapper`, `product-auditor`, `idea-generator`, `design-auditor`, `engineering-auditor`, and `quality-auditor` for applicable audit scopes. Implementation agents use matching `developer-*` IDs. Audit specialists deny file edits and shell commands in their profile while retaining read/search tools; still compare Git state before and after an audit.
- The `/improve-project` command is defined in `.opencode/commands/`. Its primary agent must load the shared skill by the exact ID `improve-project`.
- Start implementation with a new `opencode run --agent project-improver --file .improve/runs/<run-id>/handoff.md "Implement only the auto-eligible tasks in this handoff"` invocation from the repository root. Do not use `--continue`; the handoff is the carried context.
- Keep `opencode.json` user settings intact. Project agent and command definitions belong in `.opencode/` and do not require rewriting the root config.

## Missing runtime support

If a CLI, app connector, agent profile, or permission prevents a fresh session from starting, keep the reports and handoff, mark the run `ready-for-implementation`, and print the exact manual launch prompt. Do not silently fall back to implementing in the audit session.

## Official runtime references

Checked 2026-11-27; recheck syntax when updating these adapters:

- [Codex subagents and project-scoped profiles](https://developers.openai.com/codex/subagents)
- [Codex CLI](https://developers.openai.com/codex/cli)
- [OpenCode skills](https://opencode.ai/docs/skills)
- [OpenCode agents](https://opencode.ai/docs/agents)
- [OpenCode commands](https://opencode.ai/docs/commands)
- [OpenCode CLI commands](https://opencode.ai/docs/cli/commands)

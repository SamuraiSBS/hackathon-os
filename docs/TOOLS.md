# Skills, plugins, and MCP tools

This repository works without external plugins or MCP connectors. `AGENTS.md` and the workflow documents are the durable project instructions; optional tools can speed up a task but never choose the product stack or replace a brief-based decision.

## Included skills

Selected Superpowers skills are included under `.agents/skills/` and pinned to the source revision recorded in `THIRD-PARTY-NOTICES.md`. They cover brainstorming, planning, delegation, debugging, review, and verification. Follow the repository instructions when a skill's generic advice conflicts with the agreed hackathon scope. Update bundled skill files deliberately and retain their notices.

The included skill names are `using-superpowers`, `brainstorming`, `writing-plans`, `dispatching-parallel-agents`, `subagent-driven-development`, `systematic-debugging`, `receiving-code-review`, `requesting-code-review`, and `verification-before-completion`. They provide stage-specific workflows; use the ones that fit the current task and keep delegated tasks bounded by the rules in `docs/EXECUTION-AND-DELEGATION.md`.

The project also includes the portable `improve-project` skill and project-scoped Codex/OpenCode agent profiles. It works from `.agents/skills/`; only agent registration and fresh-session launch vary by runtime. See `docs/PROJECT-IMPROVEMENT-LOOP.md`.

## Optional profile tools

Plugins and their authentication belong to each user's Codex profile. Check the active session before relying on a connector; setup commands and capabilities can change, so use each provider's current official installation instructions.

- **21st** can help find and review UI references and components. It is React-oriented; choose the project stack from the brief first. Never commit API keys or OAuth credentials. Use paid features only with explicit agreement.
- **shadcn MCP** can search the public registries listed in `components.json`. Those URLs are discovery sources and do not require a React, Tailwind, or shadcn application.
- **Figma** is optional when a brief or team workflow needs a design file.
- **GitHub CLI** is optional. A user can create a project repository from the GitHub template page without installing it.
- Use browser automation only after a runnable project and a real user flow exist.

## Choosing an MCP

Prefer a built-in tool, a focused CLI, or a skill for a one-shot request. Add or enable an MCP when its session state, interactive workflow, or specialized view provides a concrete benefit. Keep the set small: MCP tool descriptions consume context even when a particular task does not need them.

Never put secrets in this repository. Do not create paid accounts, purchase components, or incur external service costs without an explicit decision for the current hackathon.

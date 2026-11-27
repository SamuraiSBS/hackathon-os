# Audit protocol

## Coverage

Inventory tracked source, project instructions, product/design briefs, tests, dependency/build configuration, and supported user-facing surfaces. Exclude secrets, dependency caches, generated/build output, minified bundles, and raw media from ordinary source reading. Inventory excluded areas so the report says what the audit could not inspect. Use screenshots or a running app for visual claims when available; label source-only visual review accurately.

Normal runs begin with a complete map. Later runs use the last map plus Git changes since the last run and trace affected callers, data paths, and UI surfaces. Run a full pass when requested or when stack/structure has changed enough to invalidate the map. A clean worktree does not prove that old findings are fixed: verify them before closing or repeating.

## Work areas

- **Project mapper:** stack, entry points, modules, important data flows, platform boundaries, and existing documentation. No improvement prescriptions unless a clear risk is evidenced.
- **Product auditor:** compare current behavior with the repository’s product promise and user scenarios. Identify supported gaps or redundancies; do not infer that a feature is unused without user/usage evidence.
- **Idea generator:** challenge assumptions and suggest differentiated additions, removals, or experiments. Label novel proposals as hypotheses unless supported by project evidence or current cited research; state what evidence would validate each proposal.
- **UX and design:** inspect the actual surfaces and important states; use the existing `impeccable` skill for a focused critique/audit when available. Consider accessibility, responsive/native behavior, empty/loading/error/recovery states, and consistency with the existing design direction.
- **Engineering:** trace correctness, architecture, duplication, dead paths, performance, dependencies, and maintainability. Ground each finding in the actual implementation.
- **Quality and reliability:** inspect failure handling, cancellation, data recovery, test strategy, platform differences, security-sensitive boundaries, and gaps in coverage. Do not claim a check ran when it did not.

An orchestrator may merge overlapping roles or skip a category when it genuinely does not apply, recording the reason. The idea generator runs during broad audits and when the project map or user asks for direction; it may be skipped during a narrow fix audit. Do not spawn an agent just to fill a fixed roster.

## Finding contract

Each finding includes:

- stable ID within the run and a short title;
- category and severity/priority;
- evidence with repository path and symbol/line or observed screen/state;
- for external research, direct URL, access date, and whether the claim is a source fact or an inference;
- user or maintenance impact;
- recommendation and bounded scope;
- confidence, estimated effort, risk, dependencies, and acceptance criteria;
- status: `auto-eligible`, `needs-user-choice`, `deferred`, `duplicate`, or `rejected`.

Label claims as **observed**, **inferred**, or **hypothesis**. Do not turn absent telemetry into evidence that a feature is unused. Do not recommend deleting a feature based only on code shape or an agent’s taste. Do not report unsupported speculative improvements as defects.

## Prioritization

Rank by user impact, confidence, effort, risk, and dependency order. Prefer a few well-supported findings to a long list of generic polish. Group compatible changes only when they share the same acceptance criteria and responsible developer. The summary names the strongest opportunity, the highest risk, work deferred for a decision, and any uninspected areas.

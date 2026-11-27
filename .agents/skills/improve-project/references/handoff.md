# Run files and handoff

All run artifacts are local and ignored by Git under `.improve/`.

```text
.improve/
  PROJECT-MAP.md
  runs/<run-id>/
    summary.md
    findings.md
    reports/
      product.md
      ideas.md
      design.md
      engineering.md
      quality.md
    handoff.md
    implementation.md
```

Use a sortable UTC run ID. Preserve earlier runs. `findings.md` is the canonical list and status ledger; `summary.md` is the short human-facing result. Reports contain each auditor’s findings and evidence. Keep private project context out of paths sent to external services.

At the top of `summary.md`, record the run state as one of: `auditing`, `ready-for-implementation`, `implementing`, `completed`, `partial`, `blocked`, or `no-auto-tasks`.

## Handoff contract

`handoff.md` contains:

1. run ID, absolute repository root, source revision, and the audit’s observed Git state;
2. links to the summary, canonical findings, and specialist reports;
3. only auto-eligible task IDs, in dependency order;
4. for each task: evidence, exact scope, files/surfaces, acceptance criteria, verification expected, dependencies, and explicit out-of-scope items;
5. deferred findings that the implementation chat must leave untouched;
6. warnings about dirty files or paths that changed after the audit.

The implementation session treats the handoff as its task contract and rechecks Git state before editing. If a task’s assumptions are stale, incomplete, or conflict with existing user changes, mark it blocked in `implementation.md` and continue with independent tasks.

## Stable task state

Use IDs such as `DESIGN-01`, `PRODUCT-02`, `ENG-03`, and `QUALITY-04` within a run. In `implementation.md`, record each task as `pending`, `in-progress`, `done`, `partial`, `blocked`, or `deferred`, with changed paths and checks actually run. The final session summary links back to the same run folder.

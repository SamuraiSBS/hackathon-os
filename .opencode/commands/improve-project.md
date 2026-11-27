---
description: Run the multi-area project improvement audit and hand off safe work
agent: project-improver
---

Load the `improve-project` skill and run the requested project improvement cycle. Treat `$ARGUMENTS` as scope or mode guidance (for example, “deep audit”). Save the map, specialist reports, findings, and handoff under `.improve/`. When auto-eligible tasks exist, start a fresh OpenCode session for implementation using the handoff; do not implement in this audit session. If no safe tasks exist, report the findings and stop.

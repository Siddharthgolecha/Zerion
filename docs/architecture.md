# Architecture

Maestaris has three actors and one shared memory.

- **Worker A** — interactive coding chat.
- **Worker B** — interactive coding chat.
- **Orchestrator** — interactive planning/review chat.
- **GitHub** — Issues, comments, branches, commits, pull requests, CI, and merged history.

The original goal is to use ordinary chat usage to perform coding work. The architecture therefore does not require a separate model API, hosted executor, polling daemon, or orchestration service.

Optional automation may assist the workflow, but it must remain optional. If an automation surface cannot write to GitHub, Maestaris accepts that limitation instead of building a second execution platform around it.

The default path stays short:

```text
Issue -> worker chat -> branch/commit/PR -> orchestrator review -> merge
```

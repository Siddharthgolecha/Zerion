<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/maestaris-logo-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="assets/maestaris-logo-light.png">
    <img src="assets/maestaris-logo-light.png" alt="Maestaris" width="420">
  </picture>
</p>

<p align="center"><strong>Chats code. GitHub remembers. Maestaris coordinates.</strong></p>

# Maestaris

Maestaris is a deliberately small workflow for using ordinary AI coding chats as persistent software workers.

It exists for one purpose: **turn your normal chat usage into real GitHub work without requiring an API-agent platform or an always-on agent runtime.**

## The model

```text
                        ┌─────────────────────┐
                        │  Orchestrator chat  │
                        │ plan / review / merge│
                        └──────────┬──────────┘
                                   │
                             GitHub Issues
                                   │
                    ┌──────────────┴──────────────┐
                    │                             │
          ┌─────────▼─────────┐         ┌────────▼──────────┐
          │ Worker chat A     │         │ Worker chat B     │
          │ code / test / PR  │         │ code / test / PR  │
          └─────────┬─────────┘         └────────┬──────────┘
                    │                             │
                    └──────────► GitHub ◄─────────┘
                           branches / commits / PRs
```

GitHub is durable memory and coordination. It is **not** a second orchestration engine.

## Core workflow

1. The orchestrator creates or prioritizes a bounded GitHub Issue.
2. Worker A or B reads the queue and posts a lightweight claim.
3. The worker creates a task branch, edits the repository, runs tests, commits, pushes, and opens or updates a PR.
4. The worker posts the PR, commit, and test result back to the Issue.
5. The orchestrator reviews the actual diff and CI, then merges or requests changes.
6. The worker moves to the next useful task when you invoke it again.

That is Maestaris.

## What Maestaris intentionally does not require

- no admission-control scheduler;
- no fair-share accounting;
- no review leases;
- no dispatcher backpressure;
- no protocol relay;
- no capability-routing engine;
- no external Laya/Jev/Codex executor;
- no separate reviewer daemon;
- no simulation or runtime-conformance layer;
- no model API keys just to make ordinary chats do coding work.

Provider scheduling can optionally remind or poll, but it is **not part of the correctness model** and must not be assumed capable of repository writes.

## Start

Create three ordinary conversations:

```text
Use Maestaris on OWNER/REPO. Act as the orchestrator.
```

```text
Use Maestaris on OWNER/REPO. Act as Worker A.
```

```text
Use Maestaris on OWNER/REPO. Act as Worker B.
```

Then create tasks in GitHub and tell a worker `continue`. A worker should spend its turn doing repository work, not designing more orchestration.

See [Quick start](docs/quickstart.md), [Protocol](docs/protocol.md), and [Architecture](docs/architecture.md).

## Design rule

> **If Maestaris infrastructure becomes more complicated than the coding work it coordinates, simplify Maestaris.**

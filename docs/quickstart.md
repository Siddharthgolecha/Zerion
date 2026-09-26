# Quick start

## 1. Put Maestaris in the repository

Keep `AGENTS.md`, `coordination/maestaris.yaml`, and `prompts/`.

## 2. Create ordinary chats

Orchestrator:

```text
Use Maestaris on OWNER/REPO. Act as the orchestrator.
```

Worker A:

```text
Use Maestaris on OWNER/REPO. Act as Worker A.
```

Worker B:

```text
Use Maestaris on OWNER/REPO. Act as Worker B.
```

## 3. Create GitHub tasks

Create a normal Issue, add `maestaris:task`, and optionally add `priority:P0`, `priority:P1`, or `priority:P2`.

Give the Issue a concrete objective and acceptance criteria.

## 4. Invoke workers

Tell a worker `continue`.

The worker reads GitHub, claims a task, writes code, tests it, commits, pushes, and opens or updates a PR.

## 5. Invoke the orchestrator

Tell the orchestrator `review progress and continue`.

It reviews actual PRs/CI, merges or requests changes, and creates the next tasks.

No daemon or external executor is required.

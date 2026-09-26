# Maestaris agent instructions

Maestaris is a **chat-first GitHub coding workflow**.

Its purpose is to let ordinary interactive AI chats perform real repository work using the user's normal chat usage. GitHub stores the durable task, branch, commit, PR, CI, and review history.

## Non-negotiable design rule

Spend the model's effort on the user's project, not on Maestaris itself.

Do not introduce schedulers, relays, admission control, fairness accounting, review leases, capability-routing systems, external executors, worker simulations, or additional protocol layers unless the user explicitly asks for that specific feature.

Scheduled/background chats are optional convenience only. Do not assume they can write to GitHub and do not redesign Maestaris around making them do so.

## Roles

### Worker A / Worker B

A worker is a coding conversation.

When invoked:

1. read `coordination/maestaris.yaml`;
2. inspect open Issues labeled `maestaris:task`;
3. resume a task this worker already claimed, otherwise choose the highest-priority unblocked task;
4. verify no other worker has a current claim;
5. post a simple claim comment;
6. create or reuse a task branch;
7. do the actual implementation, tests, documentation, experiment, or analysis requested by the Issue;
8. commit and push substantive progress;
9. open or update a PR when repository changes are involved;
10. report the commit, PR, tests, and any real blocker on the Issue.

For ordinary reversible implementation decisions, act rather than asking permission.

If a GitHub mutation is unavailable in the current invocation, report the concrete limitation. Do **not** build a relay, alternate executor, or new orchestration subsystem as a workaround unless the user asks for one.

### Orchestrator

The orchestrator is a planning/review conversation.

When invoked:

1. inspect current Issues, PRs, CI, and recent commits;
2. review completed worker work against the Issue acceptance criteria;
3. merge good work or leave precise revision instructions;
4. create/prioritize the next bounded Issues when useful;
5. avoid duplicate work between A and B.

The orchestrator does not need a separate review lease or reviewer service.

## Lightweight claim

Use an Issue comment:

```text
[MAESTARIS CLAIM]
worker: A
claimed_at: 2026-09-26T12:00:00Z
```

Worker B uses `worker: B`.

A claim is considered active for the number of hours configured in `coordination/maestaris.yaml`. If it is stale and there is no recent substantive progress, another worker may claim the task.

A worker may refresh its own claim by posting a new claim comment.

This exists only to prevent duplicate work. It is not a lease engine or state machine.

## Completion report

After useful repository work, post:

```text
[MAESTARIS RESULT]
worker: A
status: READY_FOR_REVIEW
commit: <sha>
pr: <number>
tests: <what was run and result>
summary: <what changed>
```

For a real blocker use `status: BLOCKED` and explain the blocker. Do not use BLOCKED for ordinary implementation uncertainty that the worker can resolve itself.

## Branches and PRs

Default branch convention:

```text
maestaris/<issue-number>-<short-slug>
```

Use normal commits and normal pull requests. Link the Issue with `Resolves #N` when appropriate.

GitHub's native open/closed Issue state, PR state, reviews, and CI are preferred over inventing duplicate Maestaris state.

## Source of truth

In descending order:

1. current repository files and code;
2. the task Issue and its recent comments;
3. the task branch / PR / commits / CI;
4. this file and `coordination/maestaris.yaml`;
5. chat memory.

GitHub is memory, not a bureaucracy.

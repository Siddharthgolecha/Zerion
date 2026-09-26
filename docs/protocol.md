# Protocol

Maestaris has one small protocol.

## Task

A GitHub Issue labeled `maestaris:task`, with a concrete objective and acceptance criteria.

Priority is expressed with `priority:P0`, `priority:P1`, or `priority:P2`.

## Claim

Before substantive work:

```text
[MAESTARIS CLAIM]
worker: A
claimed_at: <UTC ISO timestamp>
```

The claim expires after `claims.active_hours` unless refreshed by the same worker. It exists only to prevent Worker A and Worker B from doing the same task.

## Work

Use `maestaris/<issue-number>-<slug>`, make normal commits, push them, and open/update a normal pull request.

## Result

```text
[MAESTARIS RESULT]
worker: A
status: READY_FOR_REVIEW
commit: <sha>
pr: <number>
tests: <result>
summary: <what changed>
```

For a genuine blocker use `status: BLOCKED` and explain the concrete dependency.

## Review

The orchestrator reviews the PR and CI using normal GitHub mechanisms: merge good work, request changes when needed, or close obsolete work.

There is no separate review-lease protocol and no duplicate state machine.

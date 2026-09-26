# Manual chat operation

Maestaris is optimized for ordinary interactive conversations.

A worker chat is reusable. When invoked, it reconstructs current state from GitHub and continues.

Useful worker requests:

```text
continue
pick up the next task
review your current PR and finish it
```

Useful orchestrator request:

```text
review progress and assign the next work
```

Scheduled tasks may be used for reminders or read-only status checks, but scheduled execution is not required and is not assumed to have repository-write capability.

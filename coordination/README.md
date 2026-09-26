# Coordination

Maestaris keeps only the small amount of configuration needed for two coding chats and one orchestrator to share a GitHub repository.

- `maestaris.yaml` contains repository-wide defaults.
- `agents/` contains short role identities.
- `projects/` shows how a repository may record project-specific scope.

Live work belongs in GitHub Issues, branches, pull requests, commits, and CI. There is intentionally no second mutable task-state store.

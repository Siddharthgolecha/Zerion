# Changelog

## Chat-first reset — 2026-09-26

Maestaris returned to its original purpose: using ordinary AI chat conversations to produce real GitHub commits and pull requests.

Removed from the default architecture: admission/fair-share scheduling, dispatcher backpressure, review leases, protocol relay, capability/execution routing, runtime conformance/simulation, checkpoint/provenance/telemetry subsystems, external executor requirements, scheduler bootstrap logic, and the Python orchestration package/test matrix.

The core is now Issues, lightweight worker claims, branches/commits/PRs, CI, two coding chats, and one orchestrator chat.

Earlier implementation history remains available through Git history.

# Agent Teams

Multi-agent system defined in [[claude-config]] repo. 4 specialized roles with scoped permissions.

## Roles

### [[Planner Agent|Planner]] (Opus)
Strategic planning. Reads platform state, compliance data, and backlog. Breaks operator intent into [[Plane]] issues. **Never modifies infrastructure or compliance docs.**
Tools: Read, Grep, Glob, Bash

### [[Judge Agent|Judge]] (Opus)
Verification. Runs compliance checks, compares results against acceptance criteria, reports pass/fail. **Never modifies files — reports state only.**
Tools: Read, Grep, Glob, Bash

### [[Worker Agent|Worker]] (Sonnet)
Implementation. Scoped to a single [[Plane]] issue. Full tool access for modifying infrastructure files listed in the issue's `modifies_files` field.
Tools: Read, Grep, Glob, Bash, Edit, Write

### [[Compliance Scribe Agent|Compliance Scribe]] (Sonnet)
Documentation. Updates [[SSP]], [[SAR]], [[POA&M]], and gap-analysis artifacts after [[Judge Agent|Judge]] verification. **Only role authorized to write compliance documents.**
Tools: Read, Grep, Glob, Bash, Edit, Write

## Architecture Pattern

Separation of concerns: planning, implementation, verification, and documentation are all different agents. No single agent can both build and verify. This mirrors how real security teams should work.

## Hooks (11)

- langfuse-live-trace.sh — [[Langfuse Telemetry|Langfuse]] integration
- langfuse-prompt-hook.sh — prompt tracing
- langfuse-stop-hook.py — session stats
- langfuse-agent-hook.sh — agent lifecycle
- langfuse-trace.sh — trace export
- validate-task-completion.sh — completion gates
- enforce-plan-before-work.sh — must plan before implementing
- require-issue-gate.sh — must have [[Plane]] issue before starting
- log-agent-lifecycle.sh — lifecycle logging
- notify-session-end.sh — notifications
- notify-precompact.sh — notifications

## For the Talk

This is a major differentiator not in the talk notes yet. You're not just "using Claude" — you have a structured team of specialized agents with permission boundaries, verification gates, and observability. This is closer to how an actual security team operates than "prompt engineering."

## Observed in Action

The [[Langfuse Telemetry|Langfuse data]] shows one session (96901aa2) that spawned 12 subagents working on deduplicating CLAUDE.md across repos, creating agent role definitions, and moving gate files — all from a single operator session.

---

Tags: #agents #architecture #demo-able

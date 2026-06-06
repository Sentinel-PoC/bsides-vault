# Plane

Self-hosted project management. Deployed via [[overwatch-gitops]]/apps/plane.

## Agent Integration

[[Agent Teams]] use Plane issues as work units:
- [[Planner Agent|Planner]] breaks work into Plane issues
- [[Worker Agent|Worker]] is scoped to a single issue
- require-issue-gate.sh hook enforces this

Observed in [[Langfuse Telemetry|Langfuse data]]: agents working OPS-145, OPS-146 issues autonomously.

**Not mentioned in talk notes** — but the agent-to-issue-tracker integration is a strong demo moment.

Tags: #platform #agents #not-in-talk

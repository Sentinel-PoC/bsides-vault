# Repo Map

12 active repositories (excluding claude-code-source reference copy).

*(Commit counts pulled live from Forgejo API on June 2, 2026 — development is ongoing.)*

## Core Infrastructure

| Repo | Commits | Purpose |
|------|---------|---------|
| [[sentinel-iac]] | 1,022 | Ansible (13 roles), Terraform, CI pipelines, compliance docs |
| [[overwatch]] | 211 | OKD cluster config, Terraform VMs, agent role definitions |
| [[overwatch-gitops]] | 1,109 | ArgoCD manifests for [[Deployed Apps|31 apps]], Backstage catalog |

## Security & Compliance

| Repo | Commits | Purpose |
|------|---------|---------|
| [[compliance-vault]] | 223 | OSCAL assessments, 84 evidence files, automated collection |
| [[claude-memory]] | 29 | [[SSP]], [[SAR]], [[POA&M]], audit artifacts |

## Applications

| Repo | Commits | Purpose |
|------|---------|---------|
| [[overwatch-console]] | 58 | Custom management UI (Python + TypeScript/React) |
| [[haists-website]] | 74 | Consulting website |
| [[backstage-repo|backstage]] | 29 | Developer portal config |
| [[sentinel-unifi]] | 25 | UniFi network API integration, firewall migration |

## AI & Agent Infrastructure

| Repo | Commits | Purpose |
|------|---------|---------|
| [[claude-config]] | 58 | [[Agent Teams|Agent roles]], 11 hooks, [[Langfuse Telemetry|Langfuse]] integration |
| [[sentinel-cache]] | 68 | Session context cache, platform state snapshots |

## Other

| Repo | Commits | Purpose |
|------|---------|---------|
| overwatch-harness | 18 | Agent harness framework — actively developed |

## Totals

- ~2,924 commits as of June 2, 2026 — active development ongoing since Jan 20, 2026
- ~455,000+ lines of code/config (not re-measured at current count)
- [[Commit Stats|~25% of commits directly attributed to AI agents]] (based on 5-repo sample from original sprint)

---

Tags: #repos #evidence

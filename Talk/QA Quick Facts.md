# Q&A Quick Facts

Verified facts for answering questions without speculation.
Each fact has a source. If you don't have the source, say so.

---

## The Build

| Question | Fact | Source |
|----------|------|--------|
| How long did this take? | Active development since Jan 20, 2026 — ongoing (original sprint was Jan 20 – Apr 8, ~78 days) | git first commit |
| How many commits? | ~2,924 total across 12 repos as of June 2, 2026 (Forgejo API); original sprint ~1,400 | Forgejo API + git log |
| How many repos? | 12 active repos | Forgejo |
| How many apps running? | 31 deployed via ArgoCD | overwatch-gitops/apps/ |
| How many Ansible roles? | 13 roles in sentinel-iac | sentinel-iac/ansible/roles/ |
| How many CI pipelines? | 4 named pipelines (security, compliance, DR, DefectDojo) | sentinel-iac/ci/ |
| How many compliance docs? | 15 formal docs in sentinel-iac | sentinel-iac directory listing |
| Backstage catalog entities | ~46 | Backstage UI (verify before June 6) |
| Wazuh agents deployed | 11 | Wazuh dashboard |

---

## The AI Work

| Question | Fact | Source |
|----------|------|--------|
| What % of commits are from AI? | 25% directly attributed to AI agents (305/1,231 verified commits in original 5-repo sample) | git log, 5 repos |
| What about automation? | Another 38% from CI/pipeline bots (AI-authored config driving automated commits) | git log |
| What % are human commits? | 38% (462/1,231) — ceiling, not floor (many AI-assisted) | git log |
| Longest single agent session? | 49.3 hours (Mar 30 → Apr 1, 2026) — verified | Langfuse session 78f4a74a |
| How many tool calls in that session? | 824 tool calls, 1,273 turns | Langfuse session metadata |
| What does the agent actually do? | 60% Bash commands, 21% file ops — it executes, doesn't just write | Langfuse observations |
| Cache hit rate? | 98.4% — nearly all context loaded from cache after session start | Langfuse session metadata |
| How much would this cost at API rates? | **~$9,900 for ~34 days** (Apr 30–Jun 3): 16.3B tokens, 129,318 calls, Anthropic list prices (Opus 4.5+ = $5/$25). ~$200/mo bought ~$8,700/mo of retail compute (~43×) | Claude Code transcripts (full local record); Langfuse 13-day slice cross-validates to the digit |
| What Jim actually pays | $200/month flat subscription | Claude.ai billing |

---

## Compliance Numbers

| Question | Fact | Source |
|----------|------|--------|
| Controls assessed | 366 | SAR document |
| Control families | All 20 | SAR document |
| Compliance rate | No published score — it's a lab, not an ATO. Per-control status is tracked, every gap has a number, docs are verified not asserted | SSP / SAR / POA&M |
| Why no number? | A prior ~67% came from an assessment later found both over- *and* under-stated; the verification discipline is the story, not a self-grade | internal audit 2026-06 |
| Lines of formal compliance docs | 2,379 (SSP 763 + SAR 1,010 + POA&M 606) | file wc -l |
| Evidence files | 84 automated evidence files | compliance-vault |
| Evidence frequency | Daily automated collection | compliance-vault pipeline |
| Last collection | 2026-04-07 | compliance-vault |
| CIS benchmark scores (hosts) | 40–53% across hosts | Wazuh |
| Why are CIS scores low? | Partition layout decisions made before security stack deployed — not runtime failures | Wazuh findings |

---

## The Cost Comparison

| Question | Fact | Source |
|----------|------|--------|
| Jim's total spend on AI | ~$200/month (Claude Pro subscription) | billing |
| Hardware cost | $0 additional — servers already owned | fact |
| Infrastructure engineer salary range | $130–150k/year | industry data |
| Security engineer salary range | $120–140k/year | industry data |
| GRC analyst rate | $80–100/hour | industry data |
| What a staffed team would cost | $400–500k/year conservative | industry estimate |
| Timeline with experienced staff | 6–9 months | industry estimate |
| Jim's timeline | ~11 weeks (original sprint Jan–Apr); platform in active daily development through June 2026 | git history |

---

## The Platform

| Question | Fact | Source |
|----------|------|--------|
| Hardware models | Dell R720xd, R440, Precision 7920 | hardware inventory |
| Container platform | OKD 4.21 (OpenShift Kubernetes Distribution) | ClusterVersion CR (upgraded 4.19→4.20→4.21 on 2026-05-14) |
| Virtualization | Proxmox (3 nodes) | infrastructure |
| GitOps tool | ArgoCD | deployed apps |
| Secret management | HashiCorp Vault (SSH CA + ESO) | platform |
| Auth/SSO | Keycloak (OIDC to Grafana, ArgoCD, OKD) | platform |
| SIEM | Wazuh (11 agents, CIS benchmarking) | platform |
| Active threat blocking | CrowdSec | platform |
| K8s admission control | Kyverno (enforcement mode) | platform |
| File integrity monitoring | AIDE | platform |
| AV | ClamAV | platform |
| CI security tools | Trivy, gitleaks, tflint, yamllint, ansible-lint, DefectDojo | sentinel-iac/ci/ |
| Service mesh | Istio (mTLS) | platform |
| Container registry | Harbor | platform |
| Developer portal | Backstage | platform |
| Observability | Grafana + Prometheus + Loki + Promtail | platform |
| AI observability | Langfuse | platform |
| Backup | MinIO + Backblaze B2 offsite | platform |
| External access | Pangolin/Traefik + ACME certs | platform |
| Project tracking | Plane (self-hosted) | platform |

---

## Things That Are Uncertain — Don't Guess

| Topic | What's Uncertain |
|-------|-----------------|
| "Is this platform actually good?" | Genuinely unknown — the verification problem is real |
| Would this pass a real pen test? | Not tested |
| Are architectural decisions sound? | Unknown — no scar tissue to evaluate them |
| Have the expert reviewers weighed in? | Pending (Zulq and Shawn) |
| Full commit breakdown across all 12 repos | Totals now live-pulled (2,924 as of June 2); author breakdown % only verified for original 5-repo sample |
| Agent work before March 28 | Not instrumented in Langfuse |
| Total agent hours (full project) | Not fully measured |

---

## On the "47% AI commits" Claim

The previously cited stat was "~47% of commits are from AI agents or AI-driven automation."

**Verified breakdown from 5 repos (1,231 commits):**
- 25% direct AI (Claude/Gemini)
- 38% automation (CI/pipelines running AI-authored config)
- 38% human (includes many AI-assisted commits)

If you count automation as "AI-driven": 63% could be attributed to AI in some sense.
If you count only directly attributed AI commits: 25%.

The honest answer is: "Between 25% and 63% depending on how you define it. 25% had the AI's name on the commit. The rest is harder to categorize."

---

Tags: #talk #qa #facts #verified

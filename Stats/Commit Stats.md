# Commit Stats

Git statistics across repositories. Active development since Jan 20, 2026 — ongoing.

*(As of June 2, 2026 — commit counts pulled live from Forgejo API. Development is daily; numbers will continue to climb.)*

---

## Current Totals (Forgejo API, June 2, 2026)

Repos: all 12 active platform repos under `sentinel-admin` org.

| Repo | Commits (live) |
|------|---------------|
| overwatch-gitops | 1,109 |
| sentinel-iac | 1,022 |
| compliance-vault | 223 |
| overwatch | 211 |
| sentinel-cache | 68 |
| haists-website | 74 |
| claude-config | 58 |
| overwatch-console | 58 |
| claude-memory | 29 |
| backstage | 29 |
| sentinel-unifi | 25 |
| overwatch-harness | 18 |
| **Total (12 repos)** | **2,924** |

**~2,924 commits as of June 2, 2026, and counting.**

---

## Historical Context (for talk framing)

The original "11 weeks / ~1,400 commits" window was Jan 20 – Apr 8, 2026. That window closed at ~1,400.
The platform has continued in active daily development through June 2026 and beyond.

For the talk: either cite the original 11-week sprint (1,400 commits in 11 weeks = ~127/week) as a rate argument,
OR cite the current total (~2,924 as of talk day) as evidence of ongoing production use.
Both framings are accurate and defensible. Choose based on what you want the audience to feel.

---

## Author Breakdown (5-repo sample, 1,231 commits — baseline from Jan–Apr window)

The breakdown below is from the original verified 5-repo sample. The proportions have not been re-verified
at the new totals; the sample is still the best-sourced characterization.

| Category | Authors | Commits | % |
|----------|---------|---------|---|
| Human (Jim) | koiakoia, Jim Haist, jhaist, Koia Koia | 462 | 38% |
| AI agents | Claude, Claude Code, Claude Agent, Gemini CLI, Gemini Agent, Claude Automation | 305 | 25% |
| Automation/CI | Sentinel Admin, sentinel-admin, IAC Control, Sentinel Automation, Sentinel CI, Sentinel, Administrator, IAC Engineer | 464 | 38% |

**25% of commits are directly attributed to AI agents (Claude or Gemini).**
**38% are from automated pipelines** (CI runners, Ansible controllers, etc. — AI-authored config driving automated commits).
**38% are from Jim** — many of which were commands the AI wrote that Jim ran.

The honest framing: 25% is a floor for AI-direct. 38% human is a ceiling for purely-human work.

---

## Rate

Jan–Apr window: ~127 commits/week = ~18 commits/day across the platform.

For context: the `overwatch-gitops` repo alone (31 apps managed by ArgoCD) now has 1,109 commits —
almost double the ~620 it had at the April 8 cutoff.

---

## What Commits Don't Show

- Work where the AI wrote the code and Jim committed it under his own name
- Pair-programming sessions where the agent's output was reviewed then applied
- Design decisions, architecture choices, troubleshooting conversations
- Sessions that ran but produced no commits (investigation, planning, Q&A)

See [[Langfuse Telemetry]] for agent activity that isn't captured in git history.

---

Tags: #stats #evidence #verified

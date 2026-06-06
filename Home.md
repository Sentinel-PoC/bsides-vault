# BSides Fort Wayne 2026

**$200 and a Conversation: How AI Just Democratized Security Infrastructure**

Speaker: Jim Haist | June 6, 2026 | Purdue Fort Wayne

> "I felt gatekept. I still do. So I did this to see what I could do when nobody was controlling what I had access to."

→ Open the [[BSides Mind Map]] for the full visual map.

---

## The Talk

The [[Talk Arc]] is a 9-section arc built around one thesis: AI has eliminated the cost excuse.

| # | Section | Core Idea |
|---|---------|-----------|
| 1 | [[The Personal Story]] | T1 support, no degree, no creds — just drive |
| 2 | [[What 200 Gets You]] | Live demo of the full [[Overwatch Platform]] |
| 3 | [[The Live Demo]] | Build something with AI in front of the audience |
| 4 | [[The Cost Argument]] | $400-500k team vs $200/month |
| 5 | [[The Uncomfortable Truth]] | This cuts both ways — offensive use |
| 6 | [[The Verification Problem]] | "Is this actually good?" |
| 7 | [[AI Demystified]] | A really good dictaphone + encyclopedia |
| 8 | [[Drive Is The Differentiator]] | AI promotes thinking, doesn't remove it |
| 9 | [[The Close]] | "The cost excuse is dead." |

**▶ [[The Speech]]** — the rehearsable spine (LAND lines to memorize + riff room), built on the **friction thesis**: *"AI made security frictionless — once the friction's gone, staying exposed isn't a constraint, it's a choice."*

See also: [[Q&A Themes]] · [[QA Quick Facts]] · [[Prep Checklist]]

---

## The Platform

The [[Overwatch Platform]] runs on the [[Hardware]] cluster (R720xd, R440, Precision 7920), managed through the [[GitOps Pipeline]] and secured by the [[Security Stack]].

**Infrastructure:**
[[Proxmox]] → [[OKD]] → [[ArgoCD]] → [[Deployed Apps|31 apps]]
[[GitOps Pipeline]] · [[Istio]] · [[Backstage]] · [[Grafana Stack]] · [[Plane]]

**Security:**
[[Wazuh]] · [[Vault]] · [[Keycloak]] · [[Kyverno]] · [[CrowdSec]] · [[CI Pipeline]] · [[Falco]] · [[DefectDojo]]

**Compliance:**
[[NIST 800-53 Compliance]] — 366 controls across 20 families, moderate baseline tailored to a single-site lab. Honest about what's met and what isn't; no self-graded score (it's a lab, not an ATO).
[[SSP]] · [[SAR]] · [[POA&M]] — real OSCAL artifacts, gaps tracked not hidden

---

## The Evidence

Built across [[Repo Map|12 repositories]] with [[Commit Stats|~2,924 commits]] — active development since Jan 20, 2026 and ongoing.

- [[Commit Stats]] — ~2,924 commits as of June 2, 2026; author breakdown TBD on new total
- [[Langfuse Telemetry]] — **~34 days (Apr 30–Jun 3): 129,318 model calls · 16.3B tokens · 97.7% cache · ≈ $9.9k API-equivalent vs ~$227 actual (~43×)** — from Claude Code transcripts (complete local record); Langfuse's 13-day slice cross-validates to the digit
- [[Agent Teams]] — 4-role architecture: Planner → Worker → Judge → Compliance Scribe
- [[Cost, Labor, and the Verification Discipline]] — **sourced** cost case: $200/mo ≈ **~$9.9k/34-days** API-equivalent compute (~43×), + the Veracode "45%-and-not-improving" counter-evidence, conceded and turned

**Repos in scope:** [[sentinel-iac]] · [[overwatch-gitops]] · [[compliance-vault]]

---

## Key Lines

- "AI has democratized security at the price of $200 max."
- "The documentation is true — because I verify it, and I catch the parts that aren't."
- "The tool isn't the variable. You are."
- "Not adopting AI isn't the cautious choice. It's unilateral disarmament."
- "It's so good I can't tell if it's not good — and that's the problem."
- "Most people will use AI to ignore harder."

---

Tags: #hub #talk #platform

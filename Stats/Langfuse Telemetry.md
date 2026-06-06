# Langfuse Telemetry

Two partial snapshots — Langfuse was reset in late April, so it does **not** hold the full Jan-onward history. Both windows are honest samples, not project totals.

- **Current (primary):** live API pull, **May 21 – Jun 3, 2026 (~13 days)** — full token + cost capture.
- **Earlier:** static export, **Mar 28 – Apr 8, 2026 (11 days)** — behavioral detail (sessions, tools, quality), limited token data.

> **Fuller dataset for cost:** Langfuse only retains ~13 days. The *complete* local record is Claude Code's own transcripts — **~34 days (Apr 30 – Jun 3): 129,318 model calls, 16.3B tokens, ≈ $9,861** API-equivalent. The 13-day Langfuse numbers below are a subset that **cross-validates it to the digit** (~$290/day, 2.6× on tokens/cost/days alike). Headline cost lives in [[Cost, Labor, and the Verification Discipline]].

---

## Current window — live pull 2026-06-03 (May 21 → Jun 3, ~13 days)

| Metric | Value | How verified |
|--------|-------|-------------|
| LLM generations | **61,893** | live `observations` API, type=GENERATION |
| Total tokens | **6.24 billion** | sum of `usageDetails` across all generations |
| Cache reads | 6.07B (**97.3%**) | `cache_read_input_tokens` |
| Output tokens | 36.3M | `output` |

### Cost — what it would cost vs. what it cost

| | Value |
|---|---|
| **API-equivalent @ Anthropic list price** | **≈ $3,804** |
| **Actual cost (Max 20x subscription)** | **$200/month** (~$90 prorated for this window) |

**~42× value multiple** on the subscription for this 13-day window.

**Method (so it survives scrutiny):** computed by applying Anthropic's published per-token prices to the per-model token split — **Opus 4.5+ at $5/M in, $25/M out, $0.50/M cache-read** (Anthropic dropped Opus from $15/$75 at the 4.5 gen), Sonnet $3/$15/$0.30, Haiku $1/$5/$0.10, cache-writes at 1.25× input. Validated **to the cent**: reproduces Langfuse's own opus-4-7 cost exactly ($256.47) and Sonnet to 98.8%. The Langfuse dashboard headline ($1,674) is low only because **opus-4-8 and the `[1m]` Opus variants have no pricing configured** (they compute $0) — being fixed under OPS-1154.

### By model (this window)

| Model | Tokens | Cost @ list |
|-------|--------|-------------|
| claude-sonnet-4-6 | 2.83B | $1,395 |
| claude-opus-4-7 [1m] | 1.81B | $1,076 |
| claude-opus-4-8 [1m] | 1.28B | $1,027 |
| claude-opus-4-7 | 0.26B | $256 |
| claude-opus-4-8 | 0.04B | $44 |
| claude-haiku-4-5 | 0.02B | $6 |

The fleet mixes Opus (the heavy reasoning/build work, including 1M-context sessions) with Sonnet and Haiku for cheaper sub-tasks. 97% cache reads is *why* the cost isn't even higher — after a session establishes context, almost all subsequent input is served from cache.

See [[Cost, Labor, and the Verification Discipline]] for the full sourced argument (incl. the Veracode counter-evidence).

---

## Earlier window — static export (Mar 28 – Apr 8, 2026, 11 days)

Behavioral detail the current API pull doesn't surface. Different, older window — token/cost numbers here are *not* comparable to the current pull (this export predated full token capture).

**Session durations (verified):**

| Session ID | Dates | Duration | Tool Calls | Turns |
|------------|-------|----------|-----------|-------|
| 78f4a74a | Mar 30 → Apr 1 | **49.3 hrs** | 824 | 1,273 |
| b78dd273 | Mar 29 | 35.4 hrs | 402 | 580 |
| a6a035e6 | Apr 1 | 1.5 hrs | 279 | 397 |

The 49.3-hour session ran Monday evening to Wednesday evening without human restart — 824 tool calls, 1,273 agent turns.

**Tool breakdown (2,966 spans):** Bash 60% · File ops 21% · Messaging 7% · Web 5% · Orchestration 4% · Task mgmt 2%. *60% Bash = the agent is running commands in the terminal, not just generating text.*

**Agent quality scores (7 dims, 15 traces):** Token efficiency 0.93 · Autonomy 0.80 · Reliability 0.68 · Action density 0.57 · Tool diversity 0.54 · Recovery 0.47 · Deliberation 0.24. *Deliberation lowest — moves fast, doesn't second-guess (which is exactly why the [[The Verification Problem|verification layer]] matters).*

---

## What this data does NOT show

- **The full project.** Langfuse only retains ~13 recent days; the late-April reset wiped earlier history. This is a *representative window*, not a Jan-onward total. Don't multiply it naively — annualized figures are explicit extrapolations.
- **Whether the decisions were good.** Telemetry tracks actions and tokens, not correctness — that's what the verification discipline is for.
- **The 97%-cache caveat.** Huge token counts are mostly cheap context re-reads, inherent to agentic coding. Disclosed, not hidden.

See [[Commit Stats]] for build-time evidence across the 12 repos.

---

Tags: #stats #telemetry #evidence #verified

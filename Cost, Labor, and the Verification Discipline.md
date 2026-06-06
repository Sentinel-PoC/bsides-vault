# Cost, Labor, and the Verification Discipline

> The sourced version of the cost argument — receipts, the honest counter-evidence, and the part that actually matters. Cut from this for [[The Cost Argument]] and [[The Verification Problem]]; this page is the "show your work" reference, not the script.

Tags: #reference #cost #verification #evidence

---

## The one-line version

**A $200/month subscription did, in ~34 days, ~$9,900 of compute at retail API prices (16.3 billion tokens, 129,318 model calls) — work that would otherwise be a $400–500k, 6–9-month team build. AI didn't replace the engineer. It replaced the *typing*. The scarce, billable skill moved from building to verifying — and that one isn't automating away.**

---

## Direction 1 — The subscription vs. the compute (the value of $200)

Measured from Claude Code's own session transcripts — the complete local record, every call deduped by message ID — **Apr 30 → Jun 3 2026 (~34 days), 129,318 model calls, 16.3 billion tokens (97.7% cache reads):**

| Model | Tokens | Cost @ Anthropic list |
|---|---|---|
| opus-4-7 | 9.17B | $6,094 |
| sonnet-4-6 | 5.79B | $2,718 |
| opus-4-8 | 1.31B | $1,041 |
| haiku-4-5 | 0.04B | $8 |
| **Total (Anthropic list price)** | **16.3B** | **≈ $9,861** |

**Actual cost for that window: ~$227** (a $200/month Max subscription over ~34 days). That's a **~43× value multiple** — ~$200/month bought the equivalent of **~$8,700/month** of retail compute.

**Why this is the right dataset:** the transcripts are the most complete source — they log *every* assistant call (including subagents) straight from Claude Code, with no collector drops and no gap from the late-April Langfuse reset. The Langfuse instance only retains ~13 recent days; that slice (6.24B tokens, $3,804) **cross-validates this to the digit** — identical per-day rate (~$290/day): 2.6× on tokens, cost, *and* days alike. (The full Jan-20-onward project is larger still but unrecoverable — 30-day transcript retention pruned it; this ~34-day window is the largest honest dataset.)

**Method note (so it survives scrutiny):** Anthropic's published per-token prices — **Opus 4.5+ at $5/M input, $25/M output, $0.50/M cache-read** (Anthropic dropped Opus from $15/$75 at the 4.5 generation), Sonnet $3/$15/$0.30, Haiku $1/$5/$0.10, cache-writes at 1.25× input. Validated to the cent against Langfuse's own opus-4-7 figure ($256.47).

---

## Direction 2 — AI vs. traditional labor

The same posture — IaC, Kubernetes/GitOps, secrets management, SIEM, NIST-anchored compliance-as-code — priced the old way is **$400–500k/year in salaries + 6–9 months** before it's usable.

**What actually collapsed was not the specialized knowledge. It was the time.** The expensive part of that build was never the genius — it was the *time-intensive, lower-leverage* work: typing, scaffolding, wiring boilerplate, planning out functions, translating a known design into code. That work still *matters* — but AI does it in minutes, as a force multiplier, so one person with judgment can cover ground that used to need a team of hands.

**What did NOT collapse:** deciding what to build, architecting it, knowing what "secure" means, and verifying the output is actually true. AI made the first category cheap, which makes the second category the entire job.

---

## The objection that's actually true — and why it's my argument

A security audience will (correctly) cite the data that AI-generated code is *insecure*. Concede it — completely — because conceding it is what makes everything after it credible:

- **45% of AI-generated code introduces OWASP Top 10 vulnerabilities**, across 100+ models ([Veracode 2025 GenAI Code Security Report](https://www.veracode.com/blog/genai-code-security-report/)).
- **It does not improve with newer/bigger models.** *"Two years of 'revolutionary' model releases have moved the security needle from approximately 55% to… approximately 55%"* — explicitly including Claude 4.5/4.6, GPT-5.1/5.2, Gemini 3. Functional correctness hit 95%+; security stayed flat ([Veracode Spring 2026](https://www.veracode.com/blog/spring-2026-genai-code-security/)).
- AI code: **2.74× more vulnerabilities** than human-written; **XSS slipped through 86%** of the time; Java fails ~72% ([SoftwareSeni](https://www.softwareseni.com/ai-generated-code-security-risks-why-vulnerabilities-increase-2-74x-and-how-to-prevent-them/)).

**The turn:** that is not the case against AI. It is the case *for* the verification discipline. Every one of those reports lands on the same recommendation — *"design workflows assuming AI-generated code isn't inherently secure… the human security review remains irreplaceable… treat every AI output as untrusted."* That is a verbatim description of what this lab is. **Vibe coding ships the 45%. This doesn't.**

> "45% of raw AI code is vulnerable, and it hasn't improved in two years across every frontier model. That's not my counterargument — that's my whole point. You don't ship the 45%. You build the structure that catches it."

---

## The verification discipline (the actual product)

The differentiator was never "I can use AI." Anyone can rent the $200 tier. It's the discipline that makes the output something you can stand behind:

- **Don't accept assertions — from AI *or* people.** Everyone (every model, every vendor, every prior consultant) ships confident errors. AI didn't introduce fallibility; it made *skipping verification* expensive enough to finally see.
- **Verify behaviorally and deterministically**, not by eyeballing — because eyeballing doesn't catch the 45% either. Deterministic tooling (SAST, policy engines, compliance checks), an independent judge in a clean context that doesn't trust the builder, and checks against ground truth, not against the document's own claims.
- **Boundary-honesty is the deliverable.** Not "it's all good" (that's the overconfidence you'd distrust) — but *"here's what's verified, here's what isn't, here's what we couldn't check yet."* That honesty is the thing neither naive-trust nor helpless-distrust can sell.

**Proof, from a single real session:** the AI agents generated polished, gate-passing NIST documentation that **confidently claimed controls that did not exist** — a ClamAV antivirus deployment the platform had *deliberately never installed*, audit-log tamper alarms that weren't wired, and a DR site documented with *"an RPi 5 cluster providing Kubernetes-capable compute"* that is, in reality, a room with a network stack and no computer. The structure caught all of it. Catching them took zero coding skill — it took security judgment and a refusal to accept the assertion. *That* is the job. See [[The Verification Problem]] and [[HITL Cascade — Real Session Footage]].

---

## Caveats (stated up front, so they can't be used against me)

- **The cost window is ~34 days (Apr 30–Jun 3), not "since January."** Earlier history was pruned (30-day transcript retention + an April Langfuse reset). Cite it as a *representative window*, not the project total. Annualized figures are *extrapolations* — label them as such (~$8,700/month of API-equivalent compute if sustained).
- **97% cache reads.** The token count is enormous but mostly cheap context re-reads (inherent to agentic coding). Disclosed; it's why the number isn't even higher.
- **It's a counterfactual.** "$9,861 at list prices" is what the compute *would* cost on the API, not money spent.
- **The physical/organizational controls are not single-handed.** Multi-site DR, environmental controls, and rack-level physical monitoring need the real world — they are honestly scoped as *not* met on one site (see [[POA&M]] / the CP & PE controls). That honesty is the point, not a gap to hide.

---

## Sources

- [Veracode 2025 GenAI Code Security Report](https://www.veracode.com/blog/genai-code-security-report/)
- [Veracode Spring 2026 update](https://www.veracode.com/blog/spring-2026-genai-code-security/)
- [Veracode Oct 2025 — GPT-5 pulls ahead, rivals stall](https://www.veracode.com/blog/ai-code-security-october-update/)
- [CSA — AI-generated code vulnerability surge 2026](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-generated-code-vulnerability-surge-2026/)
- [SoftwareSeni — 2.74× vulnerability increase](https://www.softwareseni.com/ai-generated-code-security-risks-why-vulnerabilities-increase-2-74x-and-how-to-prevent-them/)
- Live cost figures: this lab's own Langfuse telemetry (see [[Langfuse Telemetry]])

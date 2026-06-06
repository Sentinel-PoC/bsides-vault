# The Speech

> **How to use this:** This is a *spine*, not a script. The **▶ LAND** lines are the ones to memorize and say clean — they're the rails. Everything under "riff" is yours to wander through naturally; just come back to the nearest LAND line within a breath. Rehearse the LAND lines until they're muscle memory; then you can go off-road in the moment and always find your way home.

**The one sentence (say it 3×: open, middle, close):**
> ▶ *"AI made security frictionless. And once the friction's gone, staying exposed isn't a constraint — it's a choice."*

**Thesis in one breath:** Most insecurity is a *friction* problem, not a hacker problem. AI deleted the friction. So security stopped being about budget or expertise and became about will.

**Positioning (never break this):** You are NOT a security expert and you are NOT selling security. You're a problem-solver who uses AI as a tool. The platform is *proof*, not product. Say it out loud early — it buys the whole room's trust.

---

## OPEN (~3–4 min) — disarm, then plant the flag

▶ LAND:
> *"Quick disclaimer before anything else: I'm not a security expert. I'm a Tier-1 support tech. I don't sell security services — I couldn't if I wanted to; I don't carry that liability. So I'm not here to pitch you anything. I'm here to show you what the tool makes possible — using the hardest thing I could think of to build, as proof."*

riff:
- Who you are, plainly: T1 support, Security+, no CS degree. The gap between that and what's on the screen *is* the talk.
- Name the real enemy (DBIR-accurate — say the number): *"Most of the breaches you've cleaned up weren't sophisticated. Sixty percent involve a human — a phishing click, a stolen password walking through the front door. The single biggest way in is compromised credentials. And the things that stop that — MFA, email filtering, patching, someone actually watching the logs — those are basics. They didn't get skipped because they're hard to understand. They got skipped because they had too much friction. Not a hacker problem. A friction problem."*
- ▶ LAND the thesis (1st time): *"AI made security frictionless. Once the friction's gone, staying exposed isn't a constraint — it's a choice."*
- Set up the build: *"I'm going to prove the friction is gone by building something live, with you, in the next 20 minutes. You give me the goal."*

---

## THE BUILD (~15–20 min) — the main event; narrate the thesis

You take a goal from the audience and build it live against your infra. The *point* isn't the output — it's letting them watch the friction not be there.

What to say WHILE you build:
- Narrate the collapse: *"Watch how much of this is me deciding what I want, and how little is me typing it."*
- The floor/ceiling move (the heart of it):
  > ▶ *"I built a NIST-anchored, multi-tier platform as a support tech for $200 a month. I don't say that to impress you — I say it so you feel the floor. If the ceiling is reachable by one guy with a subscription, then the shop down the street with no MFA and a firewall nobody's touched since 2019 isn't a project. It's an afternoon."*
- The cost number, said once, clean:
  > ▶ *"In about a month, $200 of subscription did roughly $9,800 of compute at retail prices — call it 40 times the value. 16 billion tokens. One person."*
- **When the AI gets something wrong (hope it does):** stop and point at it. *"There it is — that's the whole second half of the talk. It just confidently did the wrong thing and made it look right."* If it works flawlessly, you tell the story instead (next beat).

---

## THE CATCH (~4–5 min) — woven into or right after the build

This is what makes it a *security* talk and not an AI-hype talk. It's also where your honesty wins the room.

▶ LAND:
> *"Here's the part nobody selling AI will tell you. It doesn't just build as fast as you can think — it lies as fluently as it builds. My own compliance docs claimed an antivirus I deliberately never installed. My disaster-recovery site was documented with a Kubernetes cluster running on hardware that doesn't physically exist. Perfect-looking evidence, for things that are not real."*

riff:
- The resolution — your actual method, framed as a careful builder, not an expert:
  > ▶ *"AI didn't make me an expert. It made the expert optional — as long as someone stays in charge of what's true."*
- How you stay in charge (transferable to ANY business solution, not just security):
  - **Sandbox it** — give it a contained space, don't let it loose.
  - **Make it deterministic** — the best AI output isn't AI you trust, it's a script you can *audit* without trusting it.
  - **Verify against reality** — check the deployed state, not the document's claim about itself. *"My documentation is true — because I check it, and I catch the parts that aren't."*
- The honesty flex (optional, strong): *"My own CFP for this talk said 'three physical sites.' One of them is a room with a network stack and no computer in it yet. The claim ran ahead of the build — and that drift is the exact thing I'm warning you about. The structure I just described is what caught it."*

---

## CLOSE (~3 min) — the verdict

▶ LAND (the close, thesis 3rd time):
> *"So here's where we are. Budget used to be the excuse — that's off the table. Expertise used to be the excuse — that's off the table too. A support tech did this for $200 a month. What's left isn't a constraint. It's a choice. AI made security frictionless — and once the friction is gone, staying exposed is a decision someone made. Go make the other one."*

riff:
- Bring it back to the small business / the floor — the people who can now be protected.
- You're not selling — you're handing them permission and proof.
- Last line lands and you stop. Don't trail off. (Your dad's rule: say the thing, then stop talking.)

---

## LINES TO MEMORIZE (the rails — drill these)
1. *"I'm not a security expert and I'm not selling you security."*
2. *"Most insecurity is a friction problem, not a hacker problem."*
3. *"AI made security frictionless. Once the friction's gone, staying exposed isn't a constraint — it's a choice."* (×3)
4. *"If the ceiling is reachable by one guy with a subscription, your neighbor's open wifi is an afternoon."*
5. *"It lies as fluently as it builds."*
6. *"AI made the expert optional — as long as someone stays in charge of what's true."*
7. *"Budget's off the table. Expertise's off the table. What's left is will."*

## ANTI-RAMBLE TEST
Before any tangent or story: **does it serve "friction is the enemy and AI killed it"?** Yes → tell it, land it, move on. No → cut it, no matter how good. Stories orbit; they don't escape.

## HOSTILE-Q LANDMINES (stay calm, you have answers)
- *"So you're a security expert now?"* → *"No — and that's the point. I don't have to be. I have to be the one who checks the AI's work."*
- *"Three sites?"* → *"One in production, one being equipped, offsite backup, a third planned. My CFP overclaimed it present-tense — which is the talk's whole point about claims running ahead of reality."*
- *"Isn't AI-built security insecure?"* → *"45% of raw AI code is vulnerable and hasn't improved in two years — Veracode, across every frontier model. That's not my counterargument, that's my point. You don't ship the 45%. You build the structure that catches it."*
- *"What % NIST compliant?"* → *"No published score — it's a home lab, not an accredited system. The point isn't a number; it's that the gaps are tracked and the evidence is verified, not asserted."*
- *"Isn't most of this about attackers, not friction?"* → *"The data's on my side. Verizon's DBIR: 60% of breaches involve a human — stolen credentials are the #1 way in, phishing right behind. The defenses that stop those are basics that got skipped for friction. AI removes the friction. That's the whole talk."*

---

## FACTS (citable — keep these straight)
- **Breach causes — Verizon 2025 DBIR:** human element in **60%** of breaches; **stolen/compromised credentials = #1 initial vector (22%)**; phishing **16%**; vulnerability exploitation 20%; credential attacks up ~71% YoY. Misconfiguration is real but mainly a *cloud* problem — not the headline. *(This corrects an earlier draft that wrongly led with "open wifi / default firewall passwords.")*
- **AI code security — Veracode 2025 / Spring 2026:** ~**45%** of AI-generated code carries OWASP Top-10 vulns, flat across two years of frontier models (incl. Claude 4.5/4.6, GPT-5.x, Gemini 3). Use to concede-and-turn.
- **The cost number (verified this session):** ~$200/mo did **~$9,861** of compute in **~34 days** (Apr 30–Jun 3) = **~43×**; 16.3B tokens, 129,318 calls; Opus priced $5/$25 (current). Cross-validated against Langfuse.
- **The platform (true):** one production site + DR **Site 810** (networking+power provisioned, compute deploying) + Backblaze B2 offsite; third planned. NOT "three sites in production."

---

See also: [[The Personal Story]] · [[The Cost Argument]] · [[The Verification Problem]] · [[Cost, Labor, and the Verification Discipline]] · [[QA Quick Facts]]

Tags: #talk #speech #script

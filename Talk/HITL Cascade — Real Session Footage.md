---
tags: [hitl, real-process, talk-evidence, session-023]
date: 2026-05-19
session: backlog-burn-021 / session-023
---

# HITL Cascade — Real Session Footage

> **Use case for the talk:** this is what HITL actually looks like when the agent gets stuck. Not "is this OK?" gate-checking. Dialogue. The operator brings context the agent doesn't have, and that context redirects the entire approach.

---

## The setup

Mid-session, operator drops in with: *"plane still crash looping you they fixing that or"*

Agent had been wrapping up a different rat-hole (PR #294 — 8+ hours of cascading failures on a CI fix, agent had just gotten operator's A-decision to defer it). Plane question is fresh, urgent, real-user-impact (Jim's Plane workspace is unreachable when this happens).

Agent investigates, finds:

- Plane front-door HTTP 302 alive
- Plane API workspace endpoint hangs 8s+
- `plane-api-wl` deployment has 12 ReplicaSets (revisions 1274-1285)
- One pod `b54b8bd75-8nkn9` running 9h, one pod `778ff99-kcr4g` CrashLoopBackOff 34 restarts
- `ProgressDeadlineExceeded` since 3h ago

## The visible problem (PR #247 didn't fully ship)

Agent diagnoses: PR #247 (Plane stability fixes — gunicorn workers + probe timeout + Kyverno ignoreDifferences) had merged, BUT the manual `oc apply --server-side` post-merge step never ran. The argocd-cm doesn't have the kyverno-ignoreDifferences key. So:

- ArgoCD keeps detecting Kyverno-injected annotations as drift
- selfHeal triggers re-sync every few seconds
- New RS spawns with stability patch config
- Kyverno re-annotates → new drift → new RS
- 12 RSes accumulated

Agent fixes it: applies SSA patch directly to argocd-cm. Result: **patch reported "applied" but the key isn't in the CM**. Operator-managed CM reverts non-operator keys.

## First real "I got stuck" moment

Agent: *"the openshift-gitops-operator owns the CM and reverts our key. I need to patch the ArgoCD CR's extraConfig instead, not the CM directly."*

Tries that. Works. Key lands in argocd-cm.

But Plane sync STILL OutOfSync, STILL Degraded. Why? The conditions list reveals new info:

```
"Resource apps/Deployment/plane/plane-api-wl appeared 2 times among application resources."
"Failed sync attempt: Deployment.apps 'plane-beat-worker-wl' is invalid: 
 spec.template.spec.containers[0].image: Required value"
```

PR #247 wired stability patches as files in `apps/plane/` that ArgoCD treats as standalone Deployments. The patch files have only the overrides (no `image:` field). ArgoCD tries to apply them as full Deployments → fails.

PR #247's design was right; its **wiring** was wrong.

## The pause: agent reports state, doesn't escalate to a question

> "PR #247 didn't actually catch: apps/plane/ in overwatch-gitops is wired as a path-source that interprets plane-*-security-patch.yaml as standalone Deployments. Want me to write the PR now or queue for next session?"

Operator: *"yes can we get this fixed that's what im asking you to do inside the secure and best practices envelope don't ask me if you can keep fixing the thing I asked you to fix do that per the envelope"*

**This is the rule.** Once operator has set scope ("fix Plane"), the agent doesn't gate-ask on each implementation step. The "standing envelope" applies: blanket autonomy unless an action reduces security or destroys data.

## Worker dispatched, PR merged, drift partially fixed

`worker-plane-kustomization` writes `apps/plane/kustomization.yaml`, opens PR #249, judge merges in ~6 min total. Pod count drops to single healthy replica. Cluster stable.

**But:** the "appeared 2 times" warnings persist post-merge. PR #249 only got the kustomize.yaml inventory in place — kustomize still emits the patch files as duplicate Deployments. The COMPLETE fix needs another small PR moving patches into Application.spec.kustomize.patches.

Agent files task #160 (PR #249 follow-up) and surfaces state. Doesn't dispatch another worker without operator nod.

## The "wait, all PR #294 might pass now?" surprise

Throughout the Plane fix, `worker-trivy-mirror` is still running in the background — operator hadn't been told about it because agent didn't realize it was still alive. Operator pings: *"clean up idle agents please"*.

Agent does the audit, finds **4 stale workers alive** (some marked `isActive: false` in the team config but processes still running):

> *"you have to tell them to shut down after they tell you they are shutting down and also sometimes you just have to tell them to shutdown they don't tell you shit"*

Lesson logged to memory. Send formal `shutdown_request` to each.

Worker-trivy-mirror's final report reveals: **it had been working on PR #294 the whole time**, engineered around the iac-control runner hangs with three workflow-level patches (HEALTHCHECK NONE, /etc/hosts pin, --timeout 15m), pushed commit `0ab9f13`, CI now running with 4/6 BP checks PASS.

Plot twist: the A-decision deferral *might* not stick.

## The cascade gets named

CI check: still hung at 31 minutes on the new commit, same shape as before — outer-job wedge past the trivy step. The worker's clever workflow patches handled the inner-trivy hang but the **outer-job hang** is still surfacing.

Agent uses this to draw the structural map for operator. The session has now hit **8 distinct hang shapes** trying to land PR #294:

| # | Symptom | Fix | What surfaced next |
|---|---|---|---|
| 1 | nodejs missing | install | trivy missing |
| 2 | trivy missing | install | phone-home to check.trivy.dev |
| 3 | phone-home | Harbor mirror | trivy scans 2.3GB OKD installer dir |
| 4 | workspace pollution | --skip-dirs + clean:false | git clean still walks |
| 5 | git index.lock race | serialization (needs:) | gitleaks --no-git bug |
| 6 | gitleaks false-positive | remove --no-git | KSV-0118 root findings |
| 7 | root Dockerfiles | non-root migration | 6m uniform job hang |
| 8 | **current**: outer-job wedge | (workarounds tried) | unknown next layer |

Each fix was correct. Each next layer is **downstream of the same upstream cause**: shared workspace on iac-control runner. The agent calls this the "cascade pattern" — combinatorial failure modes from shared state. Operator's mental term for the same thing: *"playing whack-a-mole."*

## The redirect that mattered

Operator: *"can you manually apply 758 so we can confirm it fixes and be done with this?"*

Agent explains OPS-758 (per-worker worktrees), trade-offs honestly:

- Security: POSITIVE — eliminates a class of cross-job data exposure
- Best practices: POSITIVE — GitHub Actions default model
- Real risks: disk pressure (iac-control 85% full), in-flight job interruption, misconfig could break ALL repos' CI

Agent starts investigating runner config (read-only, low risk). Finds iac-control has only `/dev/sda1 99G 84G 15G 85%` free.

Then operator drops the **redirect**:

> *"can't we give iac control a iscsi target and have it use that for tmp or something or too slow"*

Agent answer: iSCSI solves the wrong problem (disk space, not filesystem contention) AND would be too slow (1GbE LAN ~100MB/s vs local NVMe ~3GB/s would amplify the timeouts).

Then operator drops the **REAL redirect**:

> *"well the runners with nvme are on pve4 which si not iac control and has lots of room"*

**This is the moment HITL pays off.**

The agent had been about to implement OPS-758 on iac-control. The operator's context — *"the runners that matter are on pve4, iac-control is the disk-starved one"* — completely changes the design. The right fix isn't:

- Add per-job worktrees to iac-control (agent's plan)

The right fix is:

- **Route the workload OFF iac-control to pve4 entirely** (operator's reframe)

pve4 has 3 LXC runners on NVMe with room. If we make those runners capable of every CI job, iac-control becomes a special-case runner for `iac:host`-only tasks (or gets decommissioned from active CI rotation entirely).

This isn't a "is this OK?" question. It's the operator bringing the system-level architecture knowledge the agent doesn't have, and the agent updating the design in real-time.

## What the agent could NEVER have figured out alone

The agent had:

- Access to live runner config files
- API access to enumerate jobs and statuses
- Memory of past failures
- Ability to read code

The agent did NOT have:

- Knowledge that pve4 has NVMe (hardware topology — operator built the lab)
- Knowledge that iac-control's disk profile is "tight" while pve4 is "plenty" (capacity planning — operator's call)
- The framing that iac-control is the *special-case* runner, not the default (architectural intent — operator's strategy)

Without operator's interjection, the agent would have spent ~2h implementing per-worker worktrees on iac-control, which would have:

- Worked technically
- Made iac-control's disk pressure worse
- Failed to use the pve4 capacity that was already provisioned
- Continued the wrong architecture

## The HITL pattern this session demonstrates

1. **Operator sets scope.** ("fix plane")
2. **Agent investigates, surfaces findings as DECISIONS not QUESTIONS.** (state report + recommended path + tradeoffs)
3. **Operator either:**
   - Approves the path → agent executes inside the envelope (no more asking)
   - Redirects with context the agent didn't have → agent restarts the design
4. **When agent gets stuck:** agent describes WHERE stuck + WHY + WHAT they think is possible. Operator brings architecture context. Agent updates plan.
5. **When operator gets stuck:** operator asks "what would happen if..." or "isn't there..." or "but doesn't X..." → agent does the cost/benefit analysis on the operator's hypothesis, returns honest answer (which may be "yes" or "no, here's why").

**The wrong pattern:** agent gates every action, operator gets paged for every micro-decision, operator becomes the bottleneck and gives up using AI.

**The right pattern (what happened here):** agent works inside scope autonomously, surfaces only when genuinely stuck OR when the proposed action exceeds envelope. Operator brings system-knowledge the agent can't have. Dialogue → updated plan → autonomous execution.

## What's left from this session

- Plane stabilized (user-facing fixed)
- PR #247, #248, #249 merged (real stability + security wins)
- argocd-cm patched for Kyverno-drift
- Harbor trivy-checks mirror established (general infra win, not just sentinel-iac)
- PR #294 STILL parked behind structural runner fix
- **New direction:** route workload to pve4 instead of fixing iac-control's shared workspace. To be investigated/implemented next.

The cascade isn't beaten yet. But the *approach* to beating it changed from "patch the wedged runner" to "use the provisioned-but-underutilized capacity" — and that came from the dialogue, not from the agent's analysis alone.

---

## One-line summary for the talk

> *"The AI didn't know my pve4 had NVMe. Once I told it, the whole fix became 10x simpler."*

That sentence is more valuable as evidence than a thousand "AI builds infrastructure!" demos. The lab works because Jim is in the loop where it matters, and out of the loop where it doesn't.

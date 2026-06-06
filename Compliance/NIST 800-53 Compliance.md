# NIST 800-53 Compliance

The [[Overwatch Platform]] is assessed against NIST SP 800-53 Rev 5 Moderate baseline.

## Numbers

| Metric | Value |
|--------|-------|
| Controls assessed | 366 |
| Applicable controls | 276 |
| Control families | All 20 |

Per-control status (compliant / partial / not-met) lives in the [[SSP]], [[SAR]], and [[POA&M]] — **not published as a single pass-rate.** It's a lab, not an ATO; a self-graded "% compliant" invites a number fight and shifts continuously as controls are re-validated. The story is that every gap has a tracking number and the docs are *verified, not asserted*.

## Documents

- [[SSP]] — System Security Plan (763 lines)
- [[SAR]] — Security Assessment Report (1,010 lines)
- [[POA&M]] — Plan of Action & Milestones (606 lines)
- Total: 2,379 lines of formal compliance documentation

## Evidence Collection

[[compliance-vault]] repo contains:
- OSCAL-formatted assessment results (machine-readable)
- 84 automated evidence files
- Daily automated collection (last: 2026-04-07)
- Assessment snapshots from Feb 22 and Mar 1

## Verification Layers

- [[Wazuh]] CIS benchmarking independently validates
- [[Kyverno]] enforces admission policies
- [[CI Pipeline]] scans on every commit
- Automated evidence collection removes human fudge factor

## For the Talk

Don't cite a compliance percentage — on stage or on the site. The differentiator isn't a score, it's that this platform *continuously validates* its controls and tracks every gap, where most orgs write compliance docs once and never check them again. (A prior "~67%" figure came from an assessment an internal audit later found both over- *and* under-stated — which is exactly why a single number isn't the story. The verification discipline is.)

## Honest Admissions

- The OSCAL export only emits "satisfied" findings, so a raw file count understates real status — the SSP/SAR carry the partial/not-met detail
- Architectural decisions are the weakest part — no scar tissue from production at scale
- CIS scores 40-53% on hosts (partition-related)
- This is a work in progress, not a victory lap

---

Tags: #compliance #nist #demo-able

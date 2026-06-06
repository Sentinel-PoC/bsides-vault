# System Security Plan (SSP)

763-line formal security plan for the [[Overwatch Platform]].

## Location

[[claude-memory]] repo: `SSP-overwatch-platform.md`

## Key Details

- System: Overwatch (OKD 4.21 on [[Proxmox]])
- Owner: J. Haist
- Framework: [[NIST 800-53 Compliance|NIST SP 800-53 Rev 5 Moderate]]
- Status: per-control status tracked in the [[SAR]] / [[POA&M]]; no single pass-rate published (it's a lab, not an ATO)

## Partial Finding

SC-7(5) — HTTPS egress filtering limited by TLS protocol. Compensating controls: [[OKD]] NetworkPolicies (default-deny in 6 namespaces), ufw on managed hosts, [[Istio]] service mesh.

## Updates

- Sprint 4: CP-2 elevated to Compliant
- Sprint 7: [[Vault]] TLS enabled (commit 6b1f71c)
- Session 17: [[Keycloak]] SSO deployed, 10 controls improved

---

Tags: #compliance #documentation

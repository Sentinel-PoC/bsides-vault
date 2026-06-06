# Vault

HashiCorp Vault — secrets management and SSH certificate authority for the [[Overwatch Platform]].

## Capabilities

- SSH certificate authority (short-lived certs, not static keys)
- Secrets management for [[OKD]] workloads via [[External Secrets|External Secrets Operator]]
- Audit logging (confirmed active, POA&M P1-1 CLOSED)
- TLS enabled since Sprint 7 (commit 6b1f71c)
- **Node/workload PKI for [[SPIRE]]** — issues the x.509 cert backing x509pop attestation; every agent re-attestation event logged in Vault audit log
- **Agent auth policy separation** — 4 scoped token policies (worker/judge/planner/scribe); agents receive minimum-privilege tokens via SPIRE exchange

## DR

Vault DR automation in [[sentinel-iac]]/infrastructure/vault-dr/

## Related Controls

- [[NIST 800-53 Compliance|IA family]] — Identification and Authentication
- [[NIST 800-53 Compliance|AC family]] — Access Control
- [[NIST 800-53 Compliance|AU family]] — Audit (Vault audit logging)

## Honest Admission

Talk notes mention Vault was on EOL version — verify upgrade is complete before June 6.

---

Tags: #security #secrets #demo-able

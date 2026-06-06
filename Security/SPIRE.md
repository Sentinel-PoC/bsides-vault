# SPIRE / SPIFFE — Workload Identity

**Status: Live on iac-control + workstation. All 4 agent roles auth via SPIRE. (OPS-553)**

SPIRE (SPIFFE Runtime Environment) provides cryptographic workload identity to agents without bearer tokens or standing secrets.

## What it does

- Agents receive a SPIFFE ID (URI SAN in an x.509 cert) via the SPIRE agent
- The SPIRE agent attests the workload using **x509pop** — kernel-held cert from the existing Vault PKI; no one-shot join token
- Vault auth path trusts the SPIFFE JWT/cert; agents exchange it for a scoped Vault token at runtime
- Identity is **stable across restarts**: same SPIFFE ID re-attests automatically on restart

## Why it matters for the talk

Previous NodeAttestor was join_token (one-shot). Every restart broke auth. x509pop is durable:

- Proven by a restart-survival test: spire-agent restarted, same SPIFFE ID, all 4 roles (worker/judge/planner/scribe) re-attested without operator intervention
- Zero standing secret: no bearer token stored anywhere; kernel holds the cert
- Every attestation event is logged in Vault audit log

## Scope

Runs on: iac-control (192.168.12.210), workstation (192.168.12.55).

All 4 agent roles auth exclusively via SPIRE (worker/judge/planner/scribe). Keycloak fallback removed — Keycloak is decommissioned.

## Related

- [[Vault]] — issues the x.509 cert that backs the x509pop attestation; SPIRE trust domain configured to Vault PKI
- [[Keycloak]] — was the transitional fallback; now retired
- [[Security Stack]] — SPIRE is the workload identity layer in Access Control

Tags: #security #auth #identity #demo-able

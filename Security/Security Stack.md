# Security Stack

The [[Overwatch Platform]] security architecture. Multiple overlapping layers — defense in depth, not a single tool.

## Runtime Security

- [[Wazuh]] SIEM — 11 agents, CIS benchmarking, real-time alerting
- [[CrowdSec]] — active threat intelligence and blocking
- [[Falco]] — runtime container security (not in talk notes yet)
- [[AIDE]] — file integrity monitoring on managed hosts
- [[ClamAV]] — antivirus scanning

## Access Control

- [[Vault]] — SSH certificate authority, secrets management, audit logging, node/workload PKI for SPIRE
- [[Authentik]] — SSO/OIDC federation (ArgoCD, OKD console, Harbor, DefectDojo, Forgejo, Plane); replaced Keycloak (OPS-1163)
- [[SPIRE]] — SPIFFE workload identity via x509pop; agents re-attest with stable identity across restarts, zero standing secret
- [[Kyverno]] — admission control: Pod-Security policies ENFORCE (disallow-privileged, run-as-nonroot, resource-limits, restrict-registries — block non-compliant pods); image supply-chain (digest, signature/attestation verify) in Audit
- [[NetworkPolicies]] — default-deny in 6 namespaces
- [[Istio]] — mTLS between services

**Keycloak is retired** — realm 503, pods gone. Do not list as active.

## Vulnerability Management

- [[DefectDojo]] — centralized vulnerability tracking (not in talk notes yet)
- [[CI Pipeline|7 scanning tools in CI/CD]]: Trivy, gitleaks, tflint, yamllint, ansible-lint, and more

## Observability

- [[Grafana Stack]] — Grafana/Prometheus/Loki/Promtail
- [[Langfuse]] — AI agent observability
- [[Jaeger]] — distributed tracing

## For the Talk

10+ distinct security tools, most running simultaneously. The breadth is the point — this isn't one product, it's a layered architecture. Each tool validates claims made by other tools.

---

Tags: #security #demo-able

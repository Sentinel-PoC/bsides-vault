# Deployed Apps

31 applications deployed to [[OKD]] via [[ArgoCD]] from [[overwatch-gitops]].

## Application List

### Security & Compliance
- [[Keycloak]] — SSO/OIDC
- [[Kyverno]] policies — admission control
- [[Falco]] — runtime security
- [[DefectDojo]] — vulnerability management
- [[External Secrets|External Secrets Operator]]

### Observability
- [[Grafana Stack|Monitoring]] (Grafana/Prometheus/Loki)
- Monitoring overrides
- [[Observability]] stack
- [[Jaeger]] — distributed tracing
- [[Langfuse]] — AI agent observability

### Infrastructure
- [[ArgoCD]]
- [[Harbor]] + pull secrets
- [[Istio]] control plane + mesh config
- [[Reloader]] — config reload automation
- [[Plane]] — project management
- [[Backstage]] — developer portal
- [[NetBox]] — network DCIM/IPAM
- [[Homepage]] — dashboard
- Health checker
- [[Sentinel Ops]]
- [[Overwatch Console]]

### Applications
- [[Haists Website]] (prod + dev)
- Console
- Hello World (test)
- [[Matrix]] — messaging
- [[Jellyfin]] — media
- Seedbox
- [[ntfy]] — notifications

## For the Talk

This list proves the platform is real and actively running workloads — not a one-off demo. Several of these ([[DefectDojo]], [[Falco]], [[NetBox]], [[Matrix]]) aren't even mentioned in the talk notes yet.

---

Tags: #platform #apps #demo-able

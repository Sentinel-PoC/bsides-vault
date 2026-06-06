# Overwatch Platform

Self-hosted OKD 4.21 Kubernetes platform running on [[Hardware|3-node Proxmox cluster]]. Manages containerized workloads through [[GitOps Pipeline|ArgoCD GitOps]].

## Architecture Layers

- **Virtualization:** [[Proxmox]] cluster across 3 physical hosts
- **Container Orchestration:** [[OKD]] 4.21 (Kubernetes)
- **GitOps:** [[ArgoCD]] syncing [[Deployed Apps|31 applications]] from Git
- **Service Mesh:** [[Istio]]
- **Registry:** [[Harbor]]
- **Secrets:** [[Vault]]
- **Auth:** [[Keycloak]]
- **Observability:** [[Grafana Stack]]
- **Developer Portal:** [[Backstage]]

## Security Layers

See [[Security Stack]] for the full breakdown.

## Compliance

Assessed against [[NIST 800-53 Compliance|NIST 800-53 Rev 5 Moderate baseline]] — 366 controls across all 20 families.

## Repos

Primary repos: [[sentinel-iac]], [[overwatch]], [[overwatch-gitops]]

---

Tags: #platform #architecture

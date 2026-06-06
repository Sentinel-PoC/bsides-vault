# GitOps Pipeline

Everything deployed to [[OKD]] flows through Git. [[ArgoCD]] watches [[overwatch-gitops]] and syncs desired state to the cluster.

## Flow

1. Code/config changes committed to [[Repo Map|repos]]
2. [[CI Pipeline|CI/CD pipelines]] run security scanning
3. Changes merge to main branch
4. [[ArgoCD]] detects drift and syncs to [[OKD]]
5. [[Kyverno]] validates admission policies
6. [[Istio]] handles service mesh routing

## Repos in the Pipeline

- [[sentinel-iac]] — infrastructure-as-code, Ansible, Terraform
- [[overwatch]] — cluster config
- [[overwatch-gitops]] — application manifests (31 apps)

## For the Talk

This is the "real GitOps" claim — not just scripts, but a full declarative pipeline with automated sync and policy enforcement. Can demo ArgoCD dashboard showing sync status live.

---

Tags: #platform #gitops #demo-able

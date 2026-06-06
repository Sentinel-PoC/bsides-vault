# OKD 4.21

OpenShift Kubernetes Distribution — the container orchestration layer of the [[Overwatch Platform]].

## Details

- 3-node cluster running on [[Proxmox]] VMs
- Provisioned via [[Terraform]] in [[overwatch]] repo
- Ignition files, CSR approval scripts, rebuild scripts all in git
- Workloads managed by [[ArgoCD]] from [[overwatch-gitops]]
- [[Deployed Apps|31 applications]] running

## Security Controls

- [[Kyverno]] admission policies (enforcement, not just detection)
- [[Istio]] service mesh for mTLS between services
- [[Keycloak]] OIDC for console access
- Default-deny [[NetworkPolicies]] in 6 namespaces

## Related Repos

- [[overwatch]] — cluster bootstrap, Terraform, ignition configs
- [[overwatch-gitops]] — all deployed workloads
- [[overwatch-console]] — custom management UI

---

Tags: #platform #kubernetes #demo-able

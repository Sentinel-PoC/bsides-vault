# Kyverno

Kubernetes admission control on [[OKD]]. **Mixed mode — verified live 2026-06-03** (`validationFailureAction` per ClusterPolicy):

- **Enforce** (blocks non-compliant pods at admission): `disallow-privileged-containers`, `require-run-as-nonroot`, `require-resource-limits`, `restrict-image-registries`, `inject-harbor-pull-secret`
- **Audit** (reports, does not block — staged): `require-image-digest`, `verify-image-signatures`, `verify-attestations`, `require-labels`, `require-backstage-annotations`

So **Pod-Security is genuinely enforced**; the **image supply-chain policies (digest pinning, cosign signature/attestation verification) are still Audit-only** — honest framing for the talk: don't claim signature-enforcement at admission yet. Policies in [[overwatch-gitops]]/apps/kyverno-policies. Part of the [[Security Stack]].

Tags: #security #kubernetes #demo-able

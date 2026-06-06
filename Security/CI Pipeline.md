# CI Pipeline

Security scanning integrated into [[GitOps Pipeline|the CI/CD pipeline]] across all repos.

## Scanning Tools

1. **Trivy** — container image + IaC vulnerability scanning
2. **gitleaks** — secrets detection in code
3. **tflint** — Terraform linting
4. **yamllint** — YAML validation
5. **ansible-lint** — Ansible playbook validation
6. **DefectDojo integration** — centralized vulnerability reporting
7. **Forgejo Actions** — CI runner (migrated from GitLab CI)

## Pipeline Definitions

- [[sentinel-iac]]/ci/security.yml
- [[sentinel-iac]]/ci/compliance.yml
- [[sentinel-iac]]/ci/disaster-recovery.yml
- [[sentinel-iac]]/ci/defectdojo.yml
- .forgejo/workflows/ in each repo

## For the Talk

Claim is "7 security scanning tools in CI/CD" — this is provable. Can show pipeline run output. The [[DefectDojo]] integration is a bonus not in talk notes.

---

Tags: #security #ci #demo-able

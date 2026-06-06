# Keycloak — RETIRED

**Status: Fully decommissioned as of 2026-06-03 (OPS-1163).**

The realm returns 503. Pods are gone. Do not reference as active in talk material.

## What replaced it

- **SSO/OIDC federation:** [[Authentik]] — live IdP for ArgoCD, OKD console, Harbor, DefectDojo, Forgejo, Plane
- **Agent → Vault identity:** [[SPIRE]] — x509pop workload identity; Keycloak was a transitional fallback that is now gone

## History

Deployed in Session 17; improved 10 [[NIST 800-53 Compliance|NIST controls]] at the time. Replaced by Authentik (OPS-874) and fully decommissioned (OPS-1163).

Tags: #security #auth #retired

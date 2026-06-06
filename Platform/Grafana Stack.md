# Grafana Stack

Observability layer for the [[Overwatch Platform]]. Grafana + Prometheus + Loki + Promtail.

Deployed via [[overwatch-gitops]]/apps/monitoring. Auth via [[Keycloak]] OIDC. Extensive remediation work documented in [[sentinel-cache]] (dashboard fixes, query audit, ServiceMonitor plans).

Part of the [[Security Stack]] observability layer alongside [[Jaeger]] and [[Langfuse Telemetry|Langfuse]].

Tags: #platform #observability #demo-able

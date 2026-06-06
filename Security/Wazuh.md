# Wazuh

SIEM deployed across the [[Overwatch Platform]]. Independently validates [[NIST 800-53 Compliance|compliance claims]] against actual system state.

## Current State

- 11 agents deployed across all managed hosts
- CIS benchmark scoring: 40-53% across hosts
- Proxmox hosts score lowest (partition-related failures drive ~30% of issues)
- Real-time alerting and log aggregation

## Role in Compliance

Wazuh is the independent verification layer. When the [[SSP]] says a control is implemented, Wazuh either confirms or contradicts. This is the "the documentation is true" mechanism.

Cross-references: [[SAR]], [[POA&M]]

## Config

Ansible roles in [[sentinel-iac]]: `wazuh-server` and `wazuh-agent`

## Honest Admission

CIS scores are 40-53% — not great. Be ready to explain why at the talk. The low scores are mostly partition layout decisions made before the security stack was deployed, not runtime configuration failures.

---

Tags: #security #compliance #demo-able

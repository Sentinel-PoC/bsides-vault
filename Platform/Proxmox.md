# Proxmox

Virtualization layer. 3-node cluster running on [[Hardware|Dell PowerEdge servers]].

Hosts all [[OKD]] VMs. Managed via [[Terraform]] and Ansible (role: proxmox-host in [[sentinel-iac]]).

CIS benchmark scores lowest on Proxmox hosts (40%) due to partition layout decisions made before security stack deployment. See [[Wazuh]].

Tags: #platform #virtualization

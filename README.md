<img width="1010" height="552" alt="Diagram" src="https://github.com/user-attachments/assets/0781898c-edcd-4f6d-8083-be9fe0c33472" />


# enterprise-homelab-cluster
Over the weekend, I built and hardened a 4 node enterprise virtualization cluster using Proxmox to practice real world systems administration and security operations.

# 4 Node Enterprise Proxmox VE Cluster & Security Operations Lab

## Executive Summary
Over the past weekend, I designed, deployed, and hardened a 4 node Proxmox hypervisor cluster simulating a hybrid enterprise network (`vault201.local`). Implemented Active Directory Domain Services, centralized SIEM security monitoring via Wazuh, reverse proxy routing, and automated infrastructure backup policies.

## Key Capabilities & Technical Stack
- **Virtualization & Compute:** 4 node Proxmox VE Cluster (High Availability, live snapshots, automated scheduled vzdump backups)
- **Identity & Access Management:** Windows Server 2022 Active Directory (`homelab.local`), GPO enforced endpoint hardening, mapped network shares
- **Security & Logging:** Wazuh SIEM (Docker deployment), Windows Agent log forwarding, Advanced Audit Policy GPOs (Event IDs 4625, 4720 tracking)
- **Networking & Traffic Control:** Nginx Proxy Manager (Reverse Proxy with custom DNS routing), Pi-hole DNS sinkhole

## Cluster Architecture
| Node | Specs / Roles | Key Guests & Services |
| :--- | :--- | :--- |
| **Node 1** | Primary Infrastructure | Windows Server 2022 (`DC-01`), AD DS, DNS, Group Policy Management |
| **Node 2** | Application & Security Hub | Ubuntu Server (`Linux-Hub`), Docker, Wazuh SIEM Stack, Uptime Kuma |
| **Node 3** | Network & Routing | Nginx Proxy Manager (NPM), Pi-hole DNS Sinkhole |
| **Node 4** | Endpoint Compute | Windows 11 Enterprise Client (`Win11-Client`, domain-joined) |

## Security & Audit Validation
- **GPO Enforcement:** Enforced Advanced Audit Policies across the `Vault Residents` OU tracking Account Management and Sensitive Privilege Use.
- **SIEM Pipeline Verification:** Executed simulated credential failure tests (Event ID 4625) and unauthorized account creation tests (Event ID 4720), verifying real-time ingestion in the Wazuh Dashboard.

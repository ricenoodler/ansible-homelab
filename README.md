# ansible-homelab

Ansible automation for my personal homelab infrastructure, built as part of
my preparation for enterprise IT and network engineering roles.

## Infrastructure Overview

| Host | Role | OS |
|------|------|----|
| Proxmox | Hypervisor (i7-12700K, ZFS RAIDZ2) | Proxmox VE |
| DebianDelMundo | Primary Docker host (~30 containers) | Debian Bookworm |
| VaultWardenVM | Isolated password manager (VLAN 2) | Debian Bookworm |
| MonitorVM | Monitoring stack + Ansible control node | Debian Bookworm |
| Oracle VPS | External cloud server | Ubuntu 20.04 |

## Setup

### Requirements
- Ansible 13+ with Python 3.9+ on control node
- Python 3.9+ on all target hosts
- SSH key access to all hosts
- Dedicated `ansible` user with passwordless sudo on managed hosts

### Installation
```bash
python3 -m venv ~/.venv/ansible
source ~/.venv/ansible/bin/activate
pip install ansible
```

### Configuration
```bash
cp inventory.example.ini inventory.ini
# Fill in your actual IPs and paths
```

## Playbooks

| Playbook | Hosts | Description |
|----------|-------|-------------|
| `check-updates.yml` | all | Preview available updates without installing |
| `update.yml` | all | Full apt update and dist-upgrade across all hosts |
| `health-check.yml` | all | Reports disk usage, memory, and uptime per host |
## Design Decisions

- **Dedicated ansible user** on MonitorVM instead of root or a personal account,
  following enterprise least-privilege principles
- **Separate plays for Oracle VPS** due to compiled Python 3.10 environment,
  uses shell module instead of apt module to avoid python3-apt dependency issues
- **Inventory excluded from version control** via .gitignore — use
  inventory.example.ini as a template
- **All changes version controlled** from day one for auditability and reproducibility

## What's Next
- Node exporter deployment across all hosts via Ansible
- Docker container management playbooks
- Service health verification playbook

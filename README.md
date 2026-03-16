# ansible-homelab

Ansible automation for my personal homelab infrastructure.

## Infrastructure

| Host | Role | OS |
|------|------|----|
| Proxmox | Hypervisor | Proxmox VE |
| DebianDelMundo | Primary services (Docker, ~30 containers) | Debian |
| VaultWardenVM | Password manager | Debian |
| MonitorVM | Monitoring & Ansible control node | Debian |
| Oracle VPS | External server | Ubuntu 20.04 |

## Playbooks

| Playbook | Description |
|----------|-------------|
| `update.yml` | Updates all hosts via apt |

## Usage

1. Clone the repo
2. Copy `inventory.example.ini` to `inventory.ini` and fill in your values
3. Activate the virtual environment and run a playbook:
```bash
source ~/.venv/ansible/bin/activate
ansible-playbook -i inventory.ini update.yml
```

## Requirements
- Ansible 13+
- Python 3.9+ on all target hosts
- SSH key access to all hosts

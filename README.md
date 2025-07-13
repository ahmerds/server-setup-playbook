# Server Setup

A simple Ansible playbook to set up and secure Ubuntu production servers.

## What it does

This playbook automatically configures a fresh Ubuntu server with:

- **Security hardening**: SSH key authentication, disabled password login, fail2ban
- **Docker installation**: Latest Docker CE with docker-compose
- **User management**: Creates a new user with sudo privileges
- **System optimization**: Swap file, automatic updates, essential packages
- **Firewall setup**: UFW configuration (optional)

## Quick Start

1. **Update inventory**: Edit `inventory.ini` with your server IP and SSH key path
2. **Run setup**: `ansible-playbook -i inventory.ini setup.yml`

## Usage Examples

```bash
# Full server setup
ansible-playbook -i inventory.ini setup.yml

# Only security configuration
ansible-playbook -i inventory.ini setup.yml --tags security

# Only Docker installation
ansible-playbook -i inventory.ini setup.yml --tags docker

# Skip swap configuration
ansible-playbook -i inventory.ini setup.yml --skip-tags swap
```

## Configuration

Key variables in `setup.yml`:
- `new_user`: Username to create (default: 'user')
- `timezone`: Server timezone (default: 'UTC')
- `firewall_allowed_ports`: Ports to open (22, 80, 443)

## Requirements

- Ansible installed locally
- SSH access to target server as root
- SSH public key in `~/.ssh/id_rsa.pub`

## What gets installed

- Essential system packages (curl, git, htop, vim, etc.)
- Docker CE and Docker Compose
- Fail2ban for intrusion prevention
- UFW firewall (optional)
- Automatic security updates

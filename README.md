# Valkey Standalone Ansible Role

Ansible role for installing and configuring Valkey (a high-performance Redis fork) in standalone mode as a systemd service.

This role is designed for deploying single-node Valkey servers — ideal for development, testing, or lightweight production environments where clustering is not required.

## Features

- Download and install the Valkey binary
- Create a dedicated `valkey` system user and group
- Configure the `valkey.conf` file
- Setup Valkey as a managed systemd service
- Enable automatic reload/restart handlers on config change
- Support for custom bind IP, port, data directory, logs, and password authentication
- Includes retry mechanism for service restart to improve reliability

## Use Case

Deploying a standalone Valkey server on a single VM or bare-metal machine where:
- High-availability or sharding is not needed
- Lightweight memory caching or key-value storage is required
- Environment is development, testing, or small-scale production

## Role Variables

| Variable | Description | Default |
|:---------|:------------|:--------|
| `bind` | IP address on which Valkey will listen | `127.0.0.1` |
| `port` | Port number for Valkey service | `6379` |
| `data_dir` | Directory to store Valkey data | `/var/lib/valkey` |
| `log_file` | Log file path for Valkey logs | `/var/log/valkey/valkey.log` |
| `requirepass` | Password for Valkey client connections (optional) | _empty_ |

## How to Run

Make sure you have a valid inventory file with your standalone server details.

### Example Inventory 

```yaml
all:
  children:
    valkey_standalone:
      hosts:
        standalone:
          ansible_host: <public-ip>
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/your/private-key.pem
```
### Playbook Run Command

Run the playbook using this command:

```bash
ansible-playbook -i inventory.yml playbook.yml --extra-vars "target_group=valkey_standalone"

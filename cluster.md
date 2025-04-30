# Valkey Cluster Ansible Role

Ansible role for installing and configuring a Valkey (Redis-compatible) **cluster** across multiple nodes.

This role automates the deployment of a multi-node, sharded Valkey cluster with support for automatic clustering, master/replica assignment, systemd service management, and production-grade settings.

## Features

- Installs Valkey on all cluster nodes
- Creates system user and secure directories for Valkey
- Automatically configures cluster mode with required ports and node configs
- Supports custom bind IP, port, and advanced memory settings
- Tags nodes as master or replica using inventory
- Deploys Valkey as a systemd service on each node
- Includes retry logic and idempotency for repeated runs
- Compatible with `redis-cli` based cluster creation

## Use Case

Use this role to set up a Valkey cluster when:
- You need sharding for large datasets
- High availability and replication are required
- You want to automate multi-node deployments on bare-metal, VM, or cloud infrastructure
- Ideal for production workloads where distributed architecture is critical

## Role Variables

| Variable | Description | Default |
|:---------|:------------|:--------|
| `valkey_port` | Port Valkey listens on | `6379` |
| `valkey_cluster_enabled` | Enable cluster mode | `true` |
| `valkey_cluster_config_file` | Cluster config filename | `nodes.conf` |
| `valkey_cluster_node_timeout` | Node timeout in ms | `5000` |
| `valkey_config_dir` | Directory for Valkey config | `/etc/valkey` |
| `valkey_data_dir` | Directory for Valkey data | `/var/lib/valkey` |
| `valkey_log_dir` | Directory for Valkey logs | `/var/log/valkey` |
| `valkey_user` | System user for Valkey | `valkey` |
| `valkey_group` | System group for Valkey | `valkey` |
| `valkey_appendonly` | Enable AOF persistence | `"no"` |
| `valkey_maxmemory` | Memory limit for Valkey | `"256mb"` |
| `valkey_maxmemory_policy` | Eviction policy | `"allkeys-lru"` |

## Templates Used

- `templates/valkey.conf.j2` — Cluster-ready Valkey config
- `templates/valkey.service.j2` — Systemd service unit
- `templates/cluster_create.sh.j2` — Cluster formation script

## How to Run

Make sure you have a valid inventory with nodes grouped and optionally tagged with `leader` or `follower`.

### Playbook Run Command

```bash
ansible-playbook -i inventory.yml playbook.yml --extra-vars "target_group=valkey_cluster"


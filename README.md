#  Valkey Ansible Role

Ansible role for **installing and configuring Valkey** (open-source Redis fork) as a systemd service.

This role supports both **standalone** and **cluster** configurations, allowing flexible deployment for single-node or multi-node environments.

##  Role Purpose and Use Case

### Purpose:
The **Valkey Ansible Role** automates the installation and configuration of **Valkey**, an open-source Redis fork. It simplifies the deployment process, ensuring that Valkey is installed correctly, configured, and set up as a systemd service for both standalone and cluster-based environments. The role ensures that Valkey is ready for use with customizable configurations for binding IP, ports, data directories, and authentication passwords. This is ideal for users looking to deploy Valkey in a production environment or for testing/development purposes with minimal manual setup.

### Use Case:
This role is ideal for environments where you need to quickly and consistently deploy **Valkey** across multiple machines, either as a **standalone instance** for testing or development or as a **cluster setup** for high availability and scalability. Whether you're setting up a single node for small-scale use or distributing the load across multiple nodes for a fault-tolerant, high-performance application, this role provides the flexibility to deploy Valkey with ease and confidence.


---

##  Features

- Install Valkey binary
- Create Valkey user and group
- Configure `valkey.conf`
- Setup `valkey` as a systemd service
- Automatic service reload and restart via handlers
- Support for custom bind address, port, data directory, and password
- Supports both **standalone** and **cluster** configurations

---

##  Role Variables

| Variable      | Description                                          | Default       |
|:--------------|:-----------------------------------------------------|:--------------|
| `bind`        | IP address to bind Valkey server                     | `127.0.0.1`   |
| `port`        | Port on which Valkey will listen                      | `6379`        |
| `data_dir`    | Directory where Valkey will store data               | `/var/lib/valkey` |
| `log_file`    | Log file path for Valkey logs                        | `/var/log/valkey/valkey.log` |
| `requirepass` | Password for Valkey authentication (optional)       | _empty_        |

---

##  Templates

- `templates/valkey.conf.j2`: Valkey server configuration template.
- `templates/valkey.service.j2`: Systemd unit file template for Valkey service.

---

##  Usage Example

### Standalone Configuration
**Use Case**:  
A **standalone** setup is ideal when you need Valkey on a single machine or for development/testing purposes. You would use this when you're not looking to scale or deploy in a high-availability setup.

**Purpose**:  
The purpose of the standalone configuration is to deploy Valkey as a single-node instance for smaller environments where clustering or high availability is not required. It's perfect for isolated environments, testing, or for running a low-traffic service.

**Command**:
```
ansible-playbook -i inventory.yml playbook.yml --extra-vars "target_group=valkey_standalone"
```
### Cluster Configuration
**Use Case** :  
A **cluster** configuration is necessary when you need multiple Valkey nodes, typically for high availability, distributed environments, or production-scale applications. This setup is beneficial when scaling horizontally across multiple nodes or maintaining redundancy.


**Purpose** :     
The purpose of the cluster configuration is to enable high availability and fault tolerance by deploying Valkey across multiple nodes. This ensures that the service remains available even if one or more nodes fail, and can handle a larger workload or traffic volume. It's ideal for production environments where performance and uptime are critical.

**Command**:
```
ansible-playbook -i inventory.yml playbook.yml --extra-vars "target_group=valkey_cluster"
```



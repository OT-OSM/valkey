# Valkey Ansible Role - Molecule Testing in Cluster Mode

This repository contains the **Valkey** Ansible role, which is tested using **Molecule** in a **cluster mode** with multiple Docker containers. The goal is to ensure that the Valkey role functions correctly in a multi-node environment.

Molecule is a tool for testing Ansible roles, and in this case, it's used to test the Valkey role on multiple Ubuntu 22.04 nodes in Docker containers, simulating a cluster setup.

## Using a Virtual Environment (venv)
It is recommended to use a virtual environment (venv) to isolate your dependencies and avoid conflicts with system-wide Python packages.

**Navigate to the project directory and run:**
```
python3 -m venv venv
```
**Activate the Virtual Environment:**
```
source venv/bin/activate
```

## Prerequisites

Before using this Molecule setup, ensure that you have the following tools installed on your local machine:

- **Docker**: To run the containers for testing.
- **Molecule**: A tool for testing Ansible roles and playbooks in isolated environments.
- **Ansible**: Used for provisioning the Docker containers.
- **Python 3** and **pip**: Ensure Python 3 is installed along with `pip`.
- **Git**: To clone the repository.

To install Molecule with the Docker driver, run the following:

```bash
pip install molecule[docker]
```

## Molecule Configuration (molecule.yml)
The molecule.yml file defines the configuration for testing the Valkey role in cluster mode using multiple Docker containers (representing nodes in the cluster).

### The configuration includes:

**Driver**: Using Docker for containerized testing.

**Platforms**: Multiple Docker containers (valkey-node-1, valkey-node-2, valkey-node-3) running Ubuntu 22.04.

**Provisioner**: Ansible is used to provision the containers with the Valkey role.

**Verifier**: Verifies the provisioning with Ansible.

## Running Tests
Once you have the environment set up, you can run the Molecule tests to verify the Valkey Ansible role in a cluster environment. Molecule handles provisioning the containers, applying the role, and running tests.

## Running the Tests
To run the tests with Molecule, execute the following command:

```
molecule test -s cluster
```

## Running Individual Steps
### You can also run individual steps as follows:

**Create the environment (containers):**
```
molecule create
```
**Provision the environment with Ansible:**
```
molecule converge
```
**Verify the environment:**
```
molecule verify
```
**Destroy the environment:**
```
molecule destroy
```

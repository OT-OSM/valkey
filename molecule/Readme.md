# Valkey Ansible Role - Standalone Molecule Testing

This project contains a Molecule test setup for verifying the **standalone deployment** of the `valkey` role using Docker as the driver. The tests ensure the role works as expected on an Ubuntu 22.04 container.

##  Prerequisites

Before you begin:

- Python 3.8+
- Docker installed and running
- Ansible installed (`ansible-core`)
- `pip` installed

##  Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/valkey_ansible_role.git
cd valkey_ansible_role/standalone_valkey_molecule/valkey
```

### 2. Create a Python Virtual Environment
```
python3 -m venv venv
source venv/bin/activate
```
### 3. Install Required Packages
```
pip install molecule molecule-docker ansible-core docker
pip install molecule-docker 
```
### 4. Run Molecule Tests
#### Create Instance and Run Role
```
molecule create
molecule converge
```
#### Check Idempotency (optional but good practice)
```
molecule idempotence
```

#### Verify Test (if verify.yml is defined)
```
molecule verify
```

#### Destroy Instance After Testing
```
molecule destroy
```

## Notes
Ensure Docker daemon is running before executing Molecule commands.

Use virtual environment to avoid dependency issues.

After modifying molecule.yml, use molecule destroy before re-running to reset the environment.








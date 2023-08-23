# Ansible Repository for Infrastructure Management

This repository contains Ansible configurations, playbooks, and roles designed to automate and manage various infrastructure components. Presently, its main focus is on ClickHouse role management. Over time, I anticipate adding more roles and playbooks to provide a comprehensive suite of infrastructure automation tools.

## 📂 Directory Structure

```
ansible/
├── inventory/            # Houses Ansible inventory files
├── playbooks/            # Playbooks for diverse automation tasks
└── roles/                # Ansible roles for various components
    └── clickhouse/      # Role dedicated to ClickHouse role management
```


## 🚀 Current Roles

### 1. ClickHouse Role Management

This role is tailored for managing roles within ClickHouse. It facilitates the creation, deletion, and privilege granting for roles. For an in-depth understanding, refer to the [ClickHouse role's README](ansible/roles/clickhouse/README.md).

## 📖 Usage

1. **Set Up Your Inventory**
   
   Modify the files within the `inventory/` directory to match your infrastructure.

2. **Execute a Playbook**

   From the `playbooks/` directory:

   ```bash
   ansible-playbook -i ../inventory/your-inventory-file.yml your-playbook-file.yml

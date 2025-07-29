# Ansible Repository for Infrastructure Management

This repository contains Ansible configurations, playbooks, and roles designed to automate and manage various infrastructure components. Presently, its main focus is on ClickHouse role management. Over time, I anticipate adding more roles and playbooks to provide a comprehensive suite of infrastructure automation tools.

## 📂 Directory Structure

```
ansible/
├── inventory/            # Houses Ansible inventory files
├── playbooks/            # Playbooks for diverse automation tasks
└── roles/                # Ansible roles for various components
    ├── clickhouse/       # Role dedicated to ClickHouse role management
    ├── hadoop/           # Role for deploying HA Hadoop cluster
    └── format-disk-r9/   # Role for automatic disk formatting and mounting by SCSI ID
```



## 🚀 Current Roles

### 1. ClickHouse Role Management

This role is tailored for managing roles within ClickHouse. It facilitates the creation, deletion, and privilege granting for roles. For an in-depth understanding, refer to the [ClickHouse role's README](ansible/roles/clickhouse/README.md).

### 2. HA Hadoop Deployment

This role is tailored for setting up a High Availability Hadoop cluster. It manages the installation of Hadoop, setting up the master and worker nodes, and ensures the environment is correctly configured for a HA Hadoop setup. For a detailed overview and configuration guide, check out the [Hadoop role's README](ansible/roles/hadoop/README.md).

### 3. Format Disk R9

This role provides intelligent disk management for Rocky Linux 9 and higher systems. It automatically detects disks based on SCSI unit numbers, formats them with specified filesystems, and mounts them using UUID for persistent identification. The role supports both new disk formatting and existing disk resizing, making it ideal for infrastructure automation scenarios. For comprehensive documentation and usage examples, refer to the [Format Disk R9 role's README](ansible/roles/format-disk-r9/README.md).

## 📖 Usage

1. **Set Up Your Inventory**

   Modify the files within the `inventory/` directory to match your infrastructure.

2. **Execute a Playbook**

   From the `playbooks/` directory:

   ```bash
   ansible-playbook -i ../inventory/your-inventory-file.yml your-playbook-file.yml


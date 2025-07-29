# Format Disk R9 Role

This Ansible role is designed to automatically format and mount disks on Rocky Linux 9 and higher systems using SCSI ID mapping. The role provides intelligent disk management by automatically detecting disks based on their SCSI unit numbers and mounting them using UUID for persistent identification.

## 🎯 Key Features

- **Automatic SCSI ID Detection**: Maps SCSI unit numbers to physical disk devices
- **UUID-based Mounting**: Ensures persistent disk identification across reboots
- **Smart Disk Management**: Automatically handles both new disk formatting and existing disk resizing
- **Flexible Configuration**: Supports multiple disk configurations with customizable parameters
- **Rocky Linux 9+ Optimized**: Specifically designed for modern Linux distributions

## 📋 Requirements

- Rocky Linux 9 or higher
- Ansible 2.9+
- `lsscsi` package installed on target hosts
- `parted`, `growpart`, `sgdisk` utilities
- Appropriate filesystem tools (`resize2fs` for ext4, `xfs_growfs` for XFS)

## 🔧 Role Variables

The role uses the `disk_partitions` variable to define disk configurations:

```yaml
disk_partitions:
  - disk_unit: 1                    # SCSI ID of the disk (matches disk_unit from Terraform)
    number: "1"                      # Partition number (default: "1")
    state: present                   # Partition state (default: present)
    fs_type: ext4                    # Filesystem type (default: xfs)
    label: gpt                       # Partition table label (default: gpt)
    resize: true                     # Enable partition resizing (default: omit)
    mount_state: "mounted"           # Mount state (default: mounted)
    mount_point: "/var/lib/kafka"    # Mount point path
    owner: cp-kafka                  # Directory owner
    group: confluent                 # Directory group
    opts: "defaults"                 # Mount options (optional)
```

## 🚀 How It Works

### 1. SCSI Controller Rescan
The role begins by rescanning SCSI controllers to detect any newly attached disks.

### 2. Disk Mapping
- Uses `lsscsi` to create a mapping between SCSI generic devices (`/dev/sgX`) and block devices (`/dev/sdX`)
- Validates that specified disks exist on the target host

### 3. Smart Disk Processing
The role intelligently handles two scenarios:

#### New Disk Formatting
For disks not yet mounted:
- Creates partitions using `parted`
- Formats filesystem
- Generates UUID-based mount entries
- Mounts the disk and sets ownership

#### Existing Disk Resizing
For already mounted disks:
- Detects available space for expansion
- Resizes partitions using `growpart`
- Expands filesystem to utilize new space
- Supports both ext4 and XFS filesystems

### 4. UUID-based Mounting
All disks are mounted using UUID instead of device names, ensuring persistent identification across reboots and device reordering.

## 📝 Usage Example

### Playbook Integration

```yaml
---
- hosts: kafka_servers
  roles:
    - role: format-disk-r9
      vars:
        disk_partitions:
          - disk_unit: 1
            fs_type: ext4
            mount_point: "/var/lib/kafka"
            owner: cp-kafka
            group: confluent
          - disk_unit: 2
            fs_type: xfs
            mount_point: "/var/lib/zookeeper"
            owner: cp-kafka
            group: confluent
```

### Standalone Playbook

```yaml
---
- hosts: all
  tasks:
    - name: Format and mount disks
      include_role:
        name: format-disk-r9
      vars:
        disk_partitions:
          - disk_unit: 1
            fs_type: ext4
            mount_point: "/data"
            owner: appuser
            group: appgroup
```

## 🔍 Troubleshooting

### Common Issues

1. **Disk Not Found**: Ensure the SCSI unit number matches the actual disk configuration
2. **Permission Errors**: Verify the role has sufficient privileges to format and mount disks
3. **Filesystem Errors**: Check that appropriate filesystem tools are installed

### Debug Information

The role provides detailed logging for:
- SCSI device mapping
- Disk detection results
- Partition and filesystem operations
- Mount point status

## 📚 Dependencies

- `community.general` collection (for `parted` and `filesystem` modules)
- `ansible.posix` collection (for `mount` module)

## 🤝 Contributing

When contributing to this role:
1. Test on Rocky Linux 9+ environments
2. Ensure backward compatibility
3. Update documentation for any new features
4. Follow Ansible best practices

## 📄 License

This role is part of the Ansible infrastructure management repository. 
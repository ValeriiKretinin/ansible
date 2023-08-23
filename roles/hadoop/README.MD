# Ansible Role: HA Hadoop Deployment

This Ansible role is designed to deploy a High Availability (HA) Hadoop cluster.

## Requirements

- Ansible version > 2.9 (recommended)
- Target hosts should have `java-1.8.0-openjdk` and `java-1.8.0-openjdk-devel` (or higher versions) available in their YUM repositories.
- Target hosts should be part of the appropriate inventory groups (`hadoop-master`, `hadoop-worker`, etc.)

## Role Variables

Here are some of the main variables you can configure:

- `hadoop_maximum_am_resource_percent`: Maximum ApplicationMaster resource percent. Default is `1`.
- `hadoop_ha_nameservice_id`: Name service ID for HA setup. Default is `"hadoop-master"`.
- `hadoop_zookeeper_quorum`: Specifies the ZooKeeper quorum. Default is dynamically constructed from the `zookeeper` group.

You can also configure a number of HDFS and YARN variables, for instance:

- `hadoop.yarn.vars`: Dictionary containing YARN configuration.
- `hadoop.hdfs.vars`: Dictionary containing HDFS configuration.

Please refer to the `vars` file for a full list and more details.

## Role Tasks

1. **Java Installation**: The role starts by ensuring OpenJDK 1.8.0 is installed.
2. **Node Specific Preparations**: Depending on the type of node (master or worker), certain preparation steps are executed.
3. **JAVA_HOME Setting**: The role sets the `JAVA_HOME` environment variable for the `hadoop_user`.
4. **Hadoop Installation & Configuration**: The role checks if Hadoop is already installed and then proceeds to download, extract, and configure Hadoop if required.
5. **Environment Variable Adjustments**: The role updates `.bashrc` and `.bash_profile` for the `hadoop_user` to include Hadoop specific configurations.
6. **Master Node Configuration**: If the target host is a master node, additional configurations are applied.

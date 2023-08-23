# Ansible Role: ClickHouse Role Management

This Ansible role provides tools for managing roles within ClickHouse, offering functionalities for role creation, deletion, and the granting of privileges. It employs SQL-driven commands via the ClickHouse client, ensuring efficient and automated management of ClickHouse roles.

## Tasks Overview

1. **Previous Grants Cleaning (Optional)**
    - Optionally revokes all privileges from all users, except for those listed in the Ansible variables.
    - Helps in maintaining a fresh state before re-applying or updating user permissions.
    - *Tags*: `clickhouse_grants`, `select`, `SQL_driven`

2. **Grant Permissions & Privileges**
    - Iteratively grants permissions and privileges to roles based on the `clickhouse_custom_grants` variable.
    - *Tags*: `clickhouse_grants`

3. **Grant Roles**
    - Assigns specific roles to users derived from the `clickhouse_custom_grant_roles` variable.
    - *Tags*: `clickhouse_grants`

4. **List Existing Roles (SQL-driven)**
    - Retrieves a list of roles currently registered within ClickHouse stored in the local directory.
    - *Tags*: `clickhouse_roles`, `select`, `SQL_driven`

5. **Drop Roles (SQL-driven)**
    - Removes roles from ClickHouse that are not present in the `clickhouse_custom_roles` variable.
    - *Tags*: `clickhouse_roles`, `delete`, `SQL_driven`

6. **Add Roles (SQL-driven)**
    - Adds new roles to ClickHouse based on the `clickhouse_custom_roles` variable.
    - Utilizes the `DDL/ROLE.j2` template for crafting the SQL command.
    - *Tags*: `clickhouse_roles`, `create`, `SQL_driven`

## Security

All tasks containing sensitive information, such as the ClickHouse admin password, use the `no_log: True` directive. This ensures that critical data isn't recorded in logs.

## Variables

This role depends on multiple Ansible variables, including but not limited to:
- `clickhouse_user_admin`: Admin user for ClickHouse.
- `clickhouse_admin_password`: Password for the ClickHouse admin user.
- `clickhouse_custom_grants`: Custom-defined list of grants.
- `clickhouse_custom_grant_roles`: List of roles to grant.
- `clickhouse_custom_roles`: Custom roles to manage.

## Dependencies

For all operations, this role requires the ClickHouse client to be installed on the target system.

## Usage

Include this role in your playbook or other roles as required. Ensure all necessary variables are provided for a successful run. Always conduct tests in a staging environment before deploying to a production setup.

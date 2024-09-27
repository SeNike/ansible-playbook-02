# Ansible Playbook for Installing Clickhouse and Vector

## Overview

This Ansible playbook automates the installation and configuration of Clickhouse and Vector on designated hosts. It consists of two main parts:

1. **Clickhouse Installation**: Downloads and installs the specified versions of Clickhouse packages, creates a database, and restarts the Clickhouse service.
2. **Vector Installation**: Downloads and installs Vector, deploys its configuration files, and manages its service.

## Requirements

- Ansible (version 2.9 or later)
- Hosts defined in inventory/prod.yml  with appropriate permissions

## Parameters

### Clickhouse Parameters

- `clickhouse_version`: The version of Clickhouse to install.
- `clickhouse_packages`: A list of Clickhouse packages to download (e.g., `["clickhouse-client", "clickhouse-server"]`).

### Vector Parameters

- `vector_version`: The version of Vector to install.

### Inventory Hosts

- `clickhouse`: The group of hosts where Clickhouse will be installed.
- `vector`: The group of hosts where Vector will be installed.

## Tags

- **clickhouse**: Use this tag to run only the tasks related to Clickhouse installation.
- **vector**: Use this tag to run only the tasks related to Vector installation.
- **install**: General tag for both installations.

## Usage

To execute the playbook, run the following command:

```bash
ansible-playbook -i inventory/prod.yml site.yml
```

## Handlers

- Start Clickhouse Service: Restarts the Clickhouse service after installation or configuration changes.
- Start Vector Service: Starts the Vector service after installation or configuration changes.

## Error Handling

The playbook includes error handling to manage failures gracefully:

- The Clickhouse installation block will attempt to download a static package if the specified packages fail to download.
- The database creation command will not fail if the database already exists (checks for error code 82).

## Templates
- templates/vector.yml.j2: Template for the Vector configuration file.
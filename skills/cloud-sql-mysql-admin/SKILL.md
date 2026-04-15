---
name: cloud-sql-mysql-admin
description: Use these skills when you need to provision new Cloud SQL for MySQL instances, create databases and users, clone existing environments, and monitor the progress of infrastructure operations.
---

## Usage

All scripts can be executed using Node.js. Replace `<param_name>` and `<param_value>` with actual values.

**Bash:**
`node <skill_dir>/scripts/<script_name>.js '{"<param_name>": "<param_value>"}'`

**PowerShell:**
`node <skill_dir>/scripts/<script_name>.js '{\"<param_name>\": \"<param_value>\"}'`

Note: The scripts automatically load the environment variables from various .env files. Do not ask the user to set vars unless skill executions fails due to env var absence.


## Scripts


### create_database



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instance | string | The ID of the instance where the database will be created. | Yes |  |
| name | string | The name for the new database. Must be unique within the instance. | Yes |  |


---

### create_instance



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| name | string | The name of the instance | Yes |  |
| databaseVersion | string | The database version for MySQL. If not specified, defaults to the latest available version (e.g., MYSQL_8_4). | No | `MYSQL_8_4` |
| rootPassword | string | The root password for the instance | Yes |  |
| editionPreset | string | The edition of the instance. Can be `Production` or `Development`. This determines the default machine type and availability. Defaults to `Development`. | No | `Development` |


---

### create_user



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instance | string | The ID of the instance where the user will be created. | Yes |  |
| name | string | The name for the new user. Must be unique within the instance. | Yes |  |
| password | string | A secure password for the new user. Not required for IAM users. | No |  |
| iamUser | boolean | Set to true to create a Cloud IAM user. | Yes |  |


---

### get_instance



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| projectId | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instanceId | string | The instance ID | Yes |  |


---

### list_databases

Lists all databases for a Cloud SQL instance.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instance | string | The instance ID | Yes |  |


---

### list_instances

Lists all type of Cloud SQL instances for a project.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |


---

### wait_for_operation



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| operation | string | The operation ID | Yes |  |


---


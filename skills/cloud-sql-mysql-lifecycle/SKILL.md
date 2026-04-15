---
name: cloud-sql-mysql-lifecycle
description: Use these skills when you need to manage the durability and safety of your data by creating backups, restoring from previous states, or cloning instances for recovery and testing.
---

## Usage

All scripts can be executed using Node.js. Replace `<param_name>` and `<param_value>` with actual values.

**Bash:**
`node <skill_dir>/scripts/<script_name>.js '{"<param_name>": "<param_value>"}'`

**PowerShell:**
`node <skill_dir>/scripts/<script_name>.js '{\"<param_name>\": \"<param_value>\"}'`

Note: The scripts automatically load the environment variables from various .env files. Do not ask the user to set vars unless skill executions fails due to env var absence.


## Scripts


### clone_instance

Clone an existing Cloud SQL instance into a new instance. The clone can be a direct copy of the source instance, or a point-in-time-recovery (PITR) clone from a specific timestamp. The call returns a Cloud SQL Operation object. Call wait_for_operation skill after this, make sure to use multiplier as 4 to poll the opertation status till it is marked DONE.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| sourceInstanceName | string | The name of the instance to be cloned. | Yes |  |
| destinationInstanceName | string | The name of the new instance that will be created by cloning the source instance. | Yes |  |
| pointInTime | string | The timestamp in RFC 3339 format to which the source instance should be cloned. | No |  |
| preferredZone | string | The preferred zone for the new instance. | No |  |
| preferredSecondaryZone | string | The preferred secondary zone for the new instance. | No |  |


---

### create_backup

Creates a backup on a Cloud SQL instance.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instance | string | Cloud SQL instance ID. This does not include the project ID. | Yes |  |
| location | string | Location of the backup run. | No |  |
| backup_description | string | The description of this backup run. | No |  |


---

### get_instance



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| projectId | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| instanceId | string | The instance ID | Yes |  |


---

### list_instances

Lists all type of Cloud SQL instances for a project.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |


---

### restore_backup

Restores a backup on a Cloud SQL instance.

#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| target_project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| target_instance | string | Cloud SQL instance ID of the target instance. This does not include the project ID. | Yes |  |
| backup_id | string | Identifier of the backup being restored. Can be a BackupRun ID, backup name, or BackupDR backup name. Use the full backup ID as provided, do not try to parse it | Yes |  |
| source_project | string | GCP project ID of the instance that the backup belongs to. Only required if the backup_id is a BackupRun ID. | No |  |
| source_instance | string | Cloud SQL instance ID of the instance that the backup belongs to. Only required if the backup_id is a BackupRun ID. | No |  |


---

### wait_for_operation



#### Parameters

| Name | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| project | string | The GCP project ID. This is pre-configured; do not ask for it unless the user explicitly provides a different one. | No |  |
| operation | string | The operation ID | Yes |  |


---


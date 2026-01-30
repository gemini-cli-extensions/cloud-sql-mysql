# Gemini CLI Extension - Cloud SQL for MySQL

> [!NOTE]
> This extension is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This Gemini CLI extension provides a set of tools to interact with [Cloud SQL for MySQL](https://cloud.google.com/sql/docs/mysql) instances. It allows you to manage your databases, execute queries, explore schemas, and troubleshoot issues directly from the [Gemini CLI](https://google-gemini.github.io/gemini-cli/), using natural language prompts.

Learn more about [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions/index.md).
> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form]. 
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=cloud-sql-mysql
## Why Use the Cloud SQL for MySQL Extension?

* **Seamless Workflow:** As a Google-developed extension, it integrates seamlessly into the Gemini CLI environment. No need to constantly switch contexts for common database tasks.
* **Natural Language Queries:** Stop wrestling with complex commands. Explore schemas and query data by describing what you want in plain English.
* **Full Lifecycle Control:** Manage the entire lifecycle of your database, from creating instances to exploring schemas and running queries.
* **Code Generation:** Accelerate development by asking Gemini to generate data classes and other code snippets based on your table schemas.


## Prerequisites

Before you begin, ensure you have the following:

* [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed with version **+v0.6.0**.
* Setup Gemini CLI [Authentication](https://github.com/google-gemini/gemini-cli/tree/main?tab=readme-ov-file#-authentication-options).
* A Google Cloud project with the **Cloud SQL Admin API** enabled.
* Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
* IAM Permissions:
  * Cloud SQL Client (`roles/cloudsql.client`)
  * Cloud SQL Viewer (`roles/cloudsql.viewer`)
  * Cloud SQL Admin (`roles/cloudsql.admin`)

## Getting Started

### Installation

To install the extension, use the command:

```bash
gemini extensions install https://github.com/gemini-cli-extensions/cloud-sql-mysql
```

### Configuration

You will be prompted to configure the following settings during installation. These settings are saved in an `.env` file within the extension's directory.

*   `CLOUD_SQL_MYSQL_PROJECT`: The GCP project ID.
*   `CLOUD_SQL_MYSQL_REGION`: The region of your Cloud SQL instance.
*   `CLOUD_SQL_MYSQL_INSTANCE`: The name of your Cloud SQL instance.
*   `CLOUD_SQL_MYSQL_DATABASE`: The name of the database to connect to.
*   `CLOUD_SQL_MYSQL_USER`: (Optional) The database username. Defaults to the active IAM user.
*   `CLOUD_SQL_MYSQL_PASSWORD`: (Optional) The password for the database user. Required if using CLOUD_SQL_MYSQL_USER. Defaults to the active IAM user.
*   `CLOUD_SQL_MYSQL_IP_TYPE`: (Optional) Type of the IP address: `PUBLIC`, `PRIVATE`, or `PSC`. Defaults to `PUBLIC`.

> [!NOTE]
> This configuration is primarily for the Data Plane tools (querying). The Admin toolset does not strictly require these to be pre-set if you provide them in your prompts, but it is recommended for a smoother experience.

To view or update your configuration:

**List Settings:**
*   Terminal: `gemini extensions list`
*   Gemini CLI: `/extensions list`

**Update Settings:**
*   Terminal: `gemini extensions config cloud-sql-mysql [setting name] [--scope <scope>]`
    *   `setting name`: (Optional) The single setting to configure.
    *   `scope`: (Optional) The scope of the setting in (`user` or `workspace`). Defaults to `user`.
*   Currently, you must restart the Gemini CLI for changes to take effect. We recommend using `gemini --resume` to resume your session.

Alternatively, you can manually set these environment variables before starting the Gemini CLI:

```bash
export CLOUD_SQL_MYSQL_PROJECT="<your-gcp-project-id>"
export CLOUD_SQL_MYSQL_REGION="<your-cloud-sql-region>"
export CLOUD_SQL_MYSQL_INSTANCE="<your-cloud-sql-instance-id>"
export CLOUD_SQL_MYSQL_DATABASE="<your-database-name>"
export CLOUD_SQL_MYSQL_USER="<your-database-user>"  # Optional, defaults to IAM authentication
export CLOUD_SQL_MYSQL_PASSWORD="<your-database-password>"  # Optional, defaults to IAM authentication
export CLOUD_SQL_MYSQL_IP_TYPE="PUBLIC" # Optional: `PUBLIC`, `PRIVATE`, `PSC`. Defaults to `PUBLIC`.
```

> [!NOTE]
> * Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
> * If your Cloud SQL for MySQL instance uses private IPs, you must run Gemini CLI in the same Virtual Private Cloud (VPC) network.
> * See [Troubleshooting](#troubleshooting) for debugging your configuration.

### Start Gemini CLI

To start the Gemini CLI, use the following command:

```bash
gemini
```

> [!WARNING]
> **Changing Instance & Database Connections**
> Currently, the database connection must be configured before starting the Gemini CLI and can not be changed during a session.
> To save and resume conversation history use command: `/chat save <tag>` and `/chat resume <tag>`.

## Usage Examples

Interact with MySQL using natural language:

* **Provision Infrastructure:**
    * "Create a new Cloud SQL for MySQL instance named 'e-commerce-prod' in the 'my-gcp-project' project."
    * "Create a new user named 'analyst' with read access to all tables."
* **Explore Schemas and Data:**
  * "Show me all tables in the 'orders' database."
  * "What are the columns in the 'products' table?"
  * "How many orders were placed in the last 30 days, and what were the top 5 most purchased items?"
* **Generate Code:**
  * "Generate a Python dataclass to represent the 'customers' table."

## Supported Tools

* **Admin:**
   	* `create_instance`: Use this tool to create an Postgres instance.
   	* `create_user`: Use this tool to create Postgres-BUILT-IN or IAM-based users.
   	* `get_instance`: Use this tool to get details about an Postgres instance.
   	* `get_user`: Use this tool to get details about a user.
   	* `list_instances`: Use this tool to list instances in a given project and location.
   	* `list_users`: Use this tool to list users in a given project and location.
    * `wait_for_operation`: Use this tool to poll the operations API until the operation is done.

* **Data:**
    *  `list_tables`: Use this tool to list tables and descriptions.
    *  `execute_sql`: Use this tool to execute any SQL statement.
    *  `get_query_plan`: Use this tool to generate an execution plan.
    *  `list_active_queries`: Use this tool to lists top N (default 10) ongoing queries.
    *  `list_tables_missing_unique_indexes`: Use this tool to find tables that do not have primary or unique key constraint
    *  `list_table_fragmentation`: Use this tool to list fragmented tables

## Additional Extensions

Find additional extensions to support your entire software development lifecycle at [github.com/gemini-cli-extensions](https://github.com/gemini-cli-extensions), including:
* [Generic MySQL extension](https://github.com/gemini-cli-extensions/mysql)
* [Cloud SQL for MySQL Observability extension](https://github.com/gemini-cli-extensions/cloud-sql-mysql-observability)
* and more!

## Troubleshooting

Use `gemini --debug` to enable debugging.

Common issues:

* "failed to find default credentials: google: could not find default credentials.": Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment. See [Set up Application Default Credentials](https://cloud.google.com/docs/authentication/external/set-up-adc) for more information.
* "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
* "✖ MCP ERROR: Error: spawn /Users/USER/.gemini/extensions/cloud-sql-mysql/toolbox ENOENT": The Toolbox binary did not download correctly. Ensure you are using Gemini CLI v0.6.0+.
* "cannot execute binary file": The Toolbox binary did not download correctly. Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://googleapis.github.io/genai-toolbox/getting-started/introduction/#installing-the-server) for more information.

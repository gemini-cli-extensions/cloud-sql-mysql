# Gemini CLI Extension - Cloud SQL for MySQL

This Gemini CLI extension provides a set of tools to interact with [Cloud SQL for MySQL](https://cloud.google.com/sql/docs/mysql) instances. It allows you to manage your databases, execute queries, and explore schemas directly from the [Gemini CLI](https://google-gemini.github.io/gemini-cli/), using natural language prompts.

## Features

*   **Integrated with Gemini CLI:** As a Google-developed extension, it integrates seamlessly into the Gemini CLI environment, making security an accessible part of your workflow.
*   **Connect to Cloud SQL for MySQL:** Securely connect to your Cloud SQL for MySQL instances.
*   **Explore Database Schema:** List databases, tables, views, and schemas.
*   **Query your Database:** Execute SQL queries against your database.

## Supported Tools

🟢 list-tables: Use this tool to list tables and descriptions.
🟢 execute-sql: Use this tool to execute any SQL statement.

## Prerequisites

Before you begin, ensure you have the following:

*   [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed.
*   A Google Cloud project with the **Cloud SQL Admin API** enabled.
*   IAM Permissions

## Installation

To install the extension, use the `gemini extensions install` command:

```bash
gemini extensions install github.com/gemini-cli-extensions/cloud-sql-mysql.git
```

## Configuration

*   `CLOUD_SQL_MYSQL_PROJECT`: The GCP project ID.
*   `CLOUD_SQL_MYSQL_REGION`: The region of your Cloud SQL instance.
*   `CLOUD_SQL_MYSQL_INSTANCE`: The ID of your Cloud SQL instance.
*   `CLOUD_SQL_MYSQL_DATABASE`: The name of the database to connect to.
*   `CLOUD_SQL_MYSQL_USER`: The database username.
*   `CLOUD_SQL_MYSQL_PASSWORD`: The password for the database user.


## Usage

* Provision Infrastructure
* Explore Schemas and Data
* Generate code


## Security

This extension executes commands against your Cloud SQL for MySQL database. Always review the generated SQL queries before execution, especially for write operations.

## Disclaimer

This is not an officially supported Google product. This extension is under active development, and breaking changes may be introduced.
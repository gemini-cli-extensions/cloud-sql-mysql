# Cloud SQL for MySQL Agent Skills

> [!NOTE]
> Currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This repository provides a set of agent skills to interact with [Cloud SQL for MySQL](https://cloud.google.com/sql/docs/mysql) instances. These skills can be used with various AI agents, including [Gemini CLI](https://google-gemini.github.io/gemini-cli/), Claude Code, and Codex, to manage your databases, execute queries, explore schemas, and troubleshoot issues using natural language prompts.

> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form].
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=cloud-sql-mysql

## Table of Contents

- [Why Use Cloud SQL for MySQL Agent Skills?](#why-use-cloud-sql-for-mysql-agent-skills)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Configuration](#configuration)
  - [Installation & Usage](#installation--usage)
    - [Gemini CLI](#gemini-cli)
    - [Claude Code](#claude-code)
    - [Codex](#codex)
    - [Antigravity](#antigravity)
- [Usage Examples](#usage-examples)
- [Supported Skills](#supported-skills)
- [Additional Agent Skills](#additional-agent-skills)
- [Troubleshooting](#troubleshooting)

## Why Use Cloud SQL for MySQL Agent Skills?

- **Seamless Workflow:** Integrates seamlessly into your AI agent's environment. No need to constantly switch contexts for common database tasks.
- **Natural Language Queries:** Stop wrestling with complex commands. Explore schemas and query data by describing what you want in plain English.
- **Full Lifecycle Control:** Manage the entire lifecycle of your database, from creating instances to exploring schemas and running queries.
- **Code Generation:** Accelerate development by asking your agent to generate data classes and other code snippets based on your table schemas.

## Prerequisites

Before you begin, ensure you have the following:

- One of these AI agents installed
  - [Gemini CLI](https://github.com/google-gemini/gemini-cli) version **v0.6.0** or higher
  - [Claude Code](https://claude.com/product/claude-code) version **v2.1.94** or higher
  - [Codex](https://developers.openai.com/codex) **v0.117.0** or higher
  - [Antigravity](https://antigravity.google) **v1.14.2** or higher
- A Google Cloud project with the **Cloud SQL Admin API** enabled.
- Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
- IAM Permissions:
  - Cloud SQL Client (`roles/cloudsql.client`)
  - Cloud SQL Viewer (`roles/cloudsql.viewer`)
  - Cloud SQL Admin (`roles/cloudsql.admin`)

> [!NOTE]
> If you do not configure a specific `CLOUD_SQL_MYSQL_USER` or `CLOUD_SQL_MYSQL_PASSWORD`, these skills default to using the active local IAM user credentials. You must also add the IAM user to your Cloud SQL instance, see [Creating a database user](https://cloud.google.com/sql/docs/mysql/add-manage-iam-users#creating-a-database-user).

## Getting Started

### Configuration

Please keep these env vars handy during the installation process:

- `CLOUD_SQL_MYSQL_PROJECT`: The GCP project ID.
- `CLOUD_SQL_MYSQL_REGION`: The region of your Cloud SQL instance.
- `CLOUD_SQL_MYSQL_INSTANCE`: The ID of your Cloud SQL instance.
- `CLOUD_SQL_MYSQL_DATABASE`: The name of the database to connect to.
- `CLOUD_SQL_MYSQL_USER`: (Optional) The database username. Defaults to the active IAM user.
- `CLOUD_SQL_MYSQL_PASSWORD`: (Optional) The password for the database user.
- `CLOUD_SQL_MYSQL_IP_TYPE`: (Optional) Type of the IP address: `PUBLIC`, `PRIVATE`, or `PSC`. Defaults to `PUBLIC`.

> [!NOTE]
>
> - Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
> - If your Cloud SQL for MySQL instance uses private IPs, you must run your agent in the same Virtual Private Cloud (VPC) network.

### Installation & Usage

To start interacting with your database, install the skills for your preferred AI agent, then launch the agent and use natural language to ask questions or perform tasks.

For the latest version, check the [releases page][releases].

[releases]: https://github.com/gemini-cli-extensions/cloud-sql-mysql/releases

<!-- {x-release-please-start-version} -->

<details open>
<summary id="gemini-cli">Gemini CLI</summary>

**1. Install the extension:**

```bash
gemini extensions install https://github.com/gemini-cli-extensions/cloud-sql-mysql
```

During the installation, enter your environment vars as described in the [configuration section](#configuration).

**2. (Optional) Manage Configuration:**
To view or update your configuration in Gemini CLI:

- Terminal: `gemini extensions config cloud-sql-mysql [setting name] [--scope <scope>]`
- Gemini CLI: `/extensions list`

**3. Start the agent:**

```bash
gemini
```

_(Tip: Run `/extensions list` to verify your configuration and active extensions.)_

> [!WARNING]
> **Changing Instance & Database Connections**
> Currently, the database connection must be configured before starting the agent and can not be changed during a session.
> To save and resume conversation history in Gemini CLI use command: `/chat save <tag>` and `/chat resume <tag>`.

</details>

<details>
<summary id="claude-code">Claude Code</summary>

**1. Set env vars:**
In your terminal, set your environment vars as described in the [configuration section](#configuration).

**2. Start the agent:**

```bash
claude
```

**3. Add the marketplace:**

```bash
/plugin marketplace add https://github.com/gemini-cli-extensions/cloud-sql-mysql.git#0.2.0
```

**4. Install the plugin:**

```bash
/plugin install cloud-sql-mysql@cloud-sql-mysql-marketplace
```

_(Tip: Run `/plugin list` inside Claude Code to verify the plugin is active, or `/reload-plugins` if you just installed it.)_

</details>

<details>
<summary id="codex">Codex</summary>

**1. Clone the Repo:**

```bash
git clone --branch 0.2.0 git@github.com:gemini-cli-extensions/cloud-sql-mysql.git
```

**2. Install the plugin:**

```bash
mkdir -p ~/.codex/plugins
cp -R /absolute/path/to/cloud-sql-mysql ~/.codex/plugins/cloud-sql-mysql
```

**3. Set env vars:**
Enter your environment vars as described in the [configuration section](#configuration).

**4. Create or update marketplace.json:**
`~/.agents/plugins/marketplace.json`

```json
{
  "name": "my-data-cloud-google-marketplace",
  "interface": {
    "displayName": "Google Data Cloud Skills"
  },
  "plugins": [
    {
      "name": "cloud-sql-mysql",
      "source": {
        "source": "local",
        "path": "./plugins/cloud-sql-mysql"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Database"
    }
  ]
}
```

_(Tip: Run `codex plugin list` or use the `/plugins` interactive menu to verify your installed plugins.)_

</details>

<details>
<summary id="antigravity">Antigravity</summary>

**1. Clone the Repo:**

```bash
git clone --branch 0.2.0 https://github.com/gemini-cli-extensions/cloud-sql-mysql.git
```

**2. Install the skills:**

Choose a location for the skills:
- **Global (all workspaces):** `~/.gemini/antigravity/skills/`
- **Workspace-specific:** `<workspace-root>/.agents/skills/`

Copy the skill folders from the cloned repository's `skills/` directory to your chosen location:

```bash
cp -R cloud-sql-mysql/skills/* ~/.gemini/antigravity/skills/
```

**3. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

_(Tip: Antigravity automatically discovers skills in these directories at the start of a session.)_

</details>

<!-- {x-release-please-end} -->

## Usage Examples

Interact with Cloud SQL for MySQL using natural language:

- **Provision Infrastructure:**
  - "Create a new Cloud SQL for MySQL instance named 'e-commerce-prod' in the 'my-gcp-project' project."
  - "Create a new user named 'analyst' with read access to all tables."
- **Explore Schemas and Data:**
  - "Show me all tables in the 'orders' database."
  - "What are the columns in the 'products' table?"
  - "How many orders were placed in the last 30 days, and what were the top 5 most purchased items?"
- **Generate Code:**
  - "Generate a Python dataclass to represent the 'customers' table."

## Supported Skills

The following skills are available in this repository:

- [Cloud SQL for MySQL Admin](./skills/cloud-sql-mysql-admin/SKILL.md) - Use these skills when you need to provision new Cloud SQL for MySQL instances, create databases and users, clone existing environments, and monitor the progress of infrastructure operations.
- [Cloud SQL for MySQL Data](./skills/cloud-sql-mysql-data/SKILL.md) - Use these skills when you need to explore your database schema, execute SQL queries to interact with your data, and inspect how MySQL plans to execute your statements.
- [Cloud SQL for MySQL Lifecycle](./skills/cloud-sql-mysql-lifecycle/SKILL.md) - Use these skills when you need to manage the durability and safety of your data by creating backups, restoring from previous states, or cloning instances for recovery and testing.
- [Cloud SQL for MySQL Monitor](./skills/cloud-sql-mysql-monitor/SKILL.md) - Use these skills when you need to troubleshoot slow queries, analyze system-level PromQL metrics, and identify structural performance issues like table fragmentation or missing unique indexes.

## Additional Agent Skills

Find additional skills to support your entire software development lifecycle at [github.com/gemini-cli-extensions](https://github.com/gemini-cli-extensions), including:

- [Generic MySQL skills](https://github.com/gemini-cli-extensions/mysql)
- [Cloud SQL for MySQL Observability extension](https://github.com/gemini-cli-extensions/cloud-sql-mysql-observability)
- and more!

## Troubleshooting

Use the debug mode of your agent (e.g., `gemini --debug`) to enable debugging.

Common issues:

- "failed to find default credentials: google: could not find default credentials.": Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment. See [Set up Application Default Credentials](https://cloud.google.com/docs/authentication/external/set-up-adc) for more information.
- "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
- "✖ MCP ERROR: Error: spawn .../toolbox ENOENT": The Toolbox binary did not download correctly. Ensure you are using the latest version of your agent.
- "cannot execute binary file": The Toolbox binary did not download correctly. Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://mcp-toolbox.dev/documentation/introduction/#install-toolbox) for more information.

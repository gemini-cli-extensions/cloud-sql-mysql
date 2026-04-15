# Refactoring Database Toolsets in MCP Toolbox

## **Overview**

Current telemetry indicates that exposing agents to more than [\~20 tools leads to a collapse in reasoning accuracy (\<40%)](https://docs.google.com/document/d/1gg47e4qcXJlZ2Zd1uOl5LPtrevGP7p1RTealXk288k0/edit?tab=t.0). To align with the [**MCP Toolbox Style Guide**](https://docs.google.com/document/d/1M_W98KfCt_mfM0vJjCkd1wU9fn6EcluWhtY0qKOAHxQ/edit?resourcekey=0-21OnBgfslm3l4NJfagLveA&tab=t.0), we must refactor our "monolithic" prebuilt values into sets of **5–8 tools** organized by **Critical User Journey**.

### **Current Toolset Size Analysis**

| Database Source                         | Current Tool Count | Status         | Primary Reason for Bloat                                                                                                                  |
| :-------------------------------------- | :----------------- | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| **Looker**                              | 33                 | 🔴 Critical    | Includes full SDK (Dev, Admin, and Query).                                                                                                |
| **AlloyDB Omni**                        | 31                 | 🔴 Critical    | High overlap with Postgres \+ Columnar specific tools.                                                                                    |
| **AlloyDB Postgres**                    | 29                 | 🔴 Critical    | Mixed Data, Maintenance, and Admin tools.                                                                                                 |
| **AlloyDB Admin**                       | 10                 | 🟡 High        | Combined Cluster, Instance, and User management.                                                                                          |
| **Cloud SQL for PostgreSQL (Postgres)** | 29                 | 🔴 Critical    | Monolithic engine for data and maintenance.                                                                                               |
| **Cloud SQL Postgres Admin**            | 11                 | 🟡 High        | Combined Instance and User management.                                                                                                    |
| **BigQuery**                            | 10                 | 🟡 High        | Mixes Metadata discovery with ML Analytics.                                                                                               |
| **Cloud SQL MySQL Admin**               | 10                 | 🟡 High        | Combined Instance and User management.                                                                                                    |
| **Cloud SQL for MySQL**                 | 6                  | ✅ Optimal     | Mixes Admin lifecycle with Data exploration.                                                                                              |
| **Cloud SQL SQL Server Admin**          | 10                 | 🟡 High        | Combined Instance and User management.                                                                                                    |
| **Cloud SQL SQL Server**                | 2                  | ✅ Optimal     |                                                                                                                                           |
| **Observability (AlloyDB, Cloud SQL)**  | 2                  | ✅ Optimal     |                                                                                                                                           |
| **Healthcare API**                      | 15                 | 🟡 High→ 👌 OK | Combined FHIR and DICOM protocols. Uses toolsets: cloud_healthcare_dataset_tools cloud_healthcare_fhir_tools cloud_healthcare_dicom_tools |
| **Firestore**                           | 9                  | 🟡 High        | Mixes Data operations with Rules management.                                                                                              |
| **Spanner**                             | 4                  | ✅ Optimal     |                                                                                                                                           |
| **Dataplex**                            | 3                  | ✅ Optimal     |                                                                                                                                           |

### **Context**

This doc will propose organizing prebuilt tools into discrete tool sets optimized for use cases. This can be exposed in Toolbox in a couple ways 1\) a new prebuilt toolset i.e. ./toolbox \--prebuilt alloydb-postgres-new-name or 2\) a named toolset within a prebuilt toolset i.e. ./toolbox \--prebuilt alloydb-postgres and use MCP server endpoint /mcp/{toolset_name}. Tools can be in multiple tool sets in order to have coverage of use case tasks.

Note: please see the [Dictionary](?tab=t.dxjmda6q2112) and [Additional Context](?tab=t.dxjmda6q2112) for more background information.

Related work includes the transition from [**Toolsets** to **Groups**](https://docs.google.com/document/d/1KUw2F1_kuHffsB2RGau6Ol0puKnMh_GMF3uO8UUKwh0/edit?resourcekey=0-ixAkamQ_UUvLPg1yzcyZ7w&tab=t.0) is a strategic architectural shift designed to create a unified collection for all MCP primitives—specifically integrating both **tools, resources, and prompts** into a single logical entity. Groupings allow for logical organization of functionality (e.g. email, calendar, etc). They also enable client-side filtering \- allowing the client or user to select only the relevant functionality for a specific task. This reduces context overload and minimizes the number of tokens sent to the LLM.  
This evolution directly supports the generation of **Agent Skills**, as skills are currently produced on a per-toolset (now per-group) basis. By using the new description field in a Group definition, Toolbox can automatically populate the server instructions for the MCP server and the \--description flag required to define a skill's purpose and strategy in its SKILL.md file.

I recommend approach 2\. Users can still get all tools in the default toolset but can limit by toolset for better performance.

| Topic / Concept            | \#1 New Prebuilt Flags (--prebuilt alloydb-dbadmin)                                                                                                                                | \#2 Named Toolsets within Prebuilt (/mcp/{toolset_name})                                                                                                                                                                      |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Discoverability**        | Visibility in documentation and \--help menus.                                                                                                                                     | Visible in logs and UI. Requires users to know the specific MCP endpoint path or consult external API docs. Currently no mechanism to list available toolsets via the MCP endpoint.                                           |
| **Granularity/Complexity** | Each flag represents a "bundled" identity. Can mix-and-match flags. **Flat:** Avoids hierarchical confusion but leads to "flag explosion" as more specialized use cases are added. | Allows a single server to host multiple logical groupings (e.g., read-only, schema-mgmt, data-ops). **Hierarchical:** Supports the MCP "Primitive Grouping" standard for organized, named collections within a single server. |
| **User Experience (UX)**   | **Simple & Explicit:** One command yields one specific set of tools. Very "Unix-style" and predictable.                                                                            | **Flexible but Complex:** The default endpoint might provide "everything," while named endpoints provide subsets. Could be confusing to debug.                                                                                |
| **System Overhead**        | **Higher:** Requires separate process instances or flag-parsing logic for every "new" prebuilt name added.                                                                         | **Lower:** A single running MCP server can multiplex multiple toolsets via routing, saving resources.                                                                                                                         |
| **Tool Overlap**           | Can lead to code duplication or complex symlinking in the backend to ensure a tool exists in two "flags."                                                                          | Naturally supports overlap; the server logic simply maps the same function to multiple endpoint aliases.                                                                                                                      |
| **Skill Generation**       | **Manual-ish:** Requires a specific flag per persona; easier to map one "Flag" to one "Skill Folder".                                                                              | **Automated:** One prebuilt server can dynamically export multiple Groups as different Skills via its internal registry.                                                                                                      |
| **Backward Compatibility** | **Low:** Requires breaking changes of toolsets                                                                                                                                     | **Strong:** Does not impact existing MCP client-server URL structures.                                                                                                                                                        |

This doc will also provide a comparison to the current OneMCP tool sets in: [Data Cloud OneMCP: Tools and Commitment Dashboard](https://docs.google.com/spreadsheets/d/1rXWhXONd5xqCpU-oJJ8eTSWtL4QVm9yuavjur-p_NXY/edit?gid=1286305679#gid=1286305679)

### **Supporting Toolsets for STDIO**

We will need a flag like `./toolbox --prebuilt alloydb-postgres/ops` where alloydb-postgres is the tool-source name and ops is the toolset name.

## **Recommendation for Toolsets and Tool Names by Source**

### **AlloyDB for PostgreSQL**

| Proposed Toolset Name         | Recommended Tools                                                                                                                                                          | Count | Toolset Description                                                                                                                                                                      |
| :---------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **alloydb-postgres-admin**    | create_cluster get_cluster list_clusters create_instance get_instance list_instances database_overview wait_for_operation                                                  | 8     | Use these tools when you need to provision new AlloyDB clusters and instances, monitor their creation status, and retrieve high-level configuration or health data for the environment.  |
| **access-management**         | create_user, list_users, get_user, list_roles, list_pg_settings, database_overview                                                                                         | 6     | Use these tools when you need to manage database users, inspect permissions and roles, and verify global configuration parameters related to security and access control.                |
| **alloydb-postgres-data**     | execute_sql, list_tables, list_views, list_schemas, list_triggers, list_indexes, list_sequences, list_stored_procedure                                                     | 8     | Use these tools when you need to explore the database schema, identify objects like views and triggers, and execute custom SQL queries to interact with your data.                       |
| **alloydb-postgres-monitor**  | list_active_queries, list_query_stats, get_query_plan, get_query_metrics, get_system_metrics, long_running_transactions, list_locks, list_database_stats                   | 7     | Use these tools when you need to troubleshoot slow performance, analyze query execution plans, identify resource-heavy processes, and monitor system-level PromQL metrics.               |
| **alloydb-postgres-health**   | list_top_bloated_tables, list_invalid_indexes, list_table_stats, get_column_cardinality, list_autovacuum_configurations, list_tablespaces, database_overview, get_instance | 6     | Use these tools when you need to optimize storage, identify index issues, analyze table statistics, or manage autovacuum and tablespace configurations to maintain peak database health. |
| **alloydb-postgres-optimize** | list_available_extensions, list_installed_extensions, list_memory_configurations, list_pg_settings, database_overview, get_cluster                                         | 8     | Use these tools when you need to discover and manage PostgreSQL extensions or fine-tune engine-level settings such as memory allocation and server configuration parameters.             |
| **replication**               | replication_stats, list_replication_slots, list_publication_tables, list_instances, get_instance, database_overview                                                        | 6     | Use these tools when you need to monitor replication health, manage sync states between nodes, and ensure the high availability and data distribution of your AlloyDB cluster.           |

**OneMCP Comparison:**

- **Unique to MCP Toolbox:** Deep columnar recommendations (list_columnar_recommended_columns) and maintenance insights.
- **Missing in Toolbox:** delete_instance, update_instance, clone_cluster, export_data, import_data.
- **Alignment:** Both support core cluster and instance CRUD.

### **AlloyDB Omni**

| Proposed Toolset Name | Recommended Tools                                                                                                                                                                                   | Count | Toolset Description                                                                                                                                                      |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **data**              | execute_sql, list_tables, list_views, list_schemas, list_triggers, list_indexes, list_sequences, list_stored_procedure                                                                              | 8     | Use these tools when you need to explore the database structure, identify schema objects like views and triggers, and execute SQL queries to interact with your data.    |
| **performance**       | execute_sql, get_query_plan, list_query_stats, get_column_cardinality, list_table_stats, list_database_stats, list_active_queries                                                                   | 7     | Use these tools when you need to analyze query performance, generate execution plans, check table/column statistics, and monitor overall database activity.              |
| **monitor**           | database_overview, list_active_queries, long_running_transactions, list_locks, list_database_stats, list_pg_settings                                                                                | 7     | Use these tools when you need to troubleshoot production issues by identifying locks, tracking long-running transactions, and getting a high-level view of server state. |
| **optimize**          | list_pg_settings, list_memory_configurations, list_available_extensions, list_installed_extensions, list_autovacuum_configurations, list_columnar_configurations, list_columnar_recommended_columns | 7     | Use these tools when you need to fine-tune the database engine settings, manage extensions, or optimize the columnar engine for better analytical performance.           |
| **health**            | list_top_bloated_tables, list_invalid_indexes, list_table_stats, list_tablespaces, database_overview, list_autovacuum_configurations                                                                | 6     | Use these tools when you need to audit database health, identify storage bloat, find broken indexes, and verify tablespace or maintenance configurations.                |
| **replication**       | replication_stats, list_replication_slots, list_publication_tables, database_overview                                                                                                               | 4     | Use these tools when you need to monitor the health of database replication, manage sync states between nodes, and audit publication tables for distributed setups.      |
| **access-control**    | list_roles, list_pg_settings, database_overview                                                                                                                                                     | 3     | Use these tools when you need to manage user roles, inspect permissions, and verify security-related configuration parameters.                                           |

**OneMCP Comparison:**OneMCP can not support Omni

### **BigQuery**

| Proposed Toolset Name  | Recommended Tools                                                                          | Count | Toolset Description                                                                                                                                                                                                                  |
| :--------------------- | :----------------------------------------------------------------------------------------- | :---- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **bigquery-data**      | execute_sql list_dataset_ids list_table_ids get_dataset_info get_table_info search_catalog | 6     | Use these tools when you need to handle large-scale data exploration and dataset management. Use when users need to find data assets or run SQL at scale. Provides metadata discovery and query execution across the data warehouse. |
| **bigquery-analytics** | analyze_contribution ask_data_insights forecast search_catalog                             | 3     | Use these tools when you need to handle advanced data intelligence and predictive tasks. Use when a user asks "why" data changed or needs future projections. Provides automated insight generation and time-series forecasting.     |

**OneMCP Comparison:**

- **Unique to MCP Toolbox:** Advanced analysis tools (analyze_contribution, forecast, search_catalog).
- **Parity:** High overlap on core metadata (list_dataset_ids, list_table_ids, get_table_info).

### **Cloud SQL PostgreSQL & Standalone**

| Proposed Toolset Name | Recommended Tools                                                                                                                                                              | Count | Toolset Description                                                                                                                                                                                       |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **admin**             | create_instance, get_instance, list_instances, create_database, list_databases, create_user, wait_for_operation, clone_instance                                                | 7     | Use these tools when you need to provision new Cloud SQL instances, create databases and users, clone existing environments, and monitor the progress of long-running operations.                         |
| **lifecycle**         | create_backup, restore_backup, postgres_upgrade_precheck, wait_for_operation, database_overview, get_instance, list_instances                                                  | 8     | Use these tools when you need to manage the lifecycle of your instances, including performing backups and restores, checking major version upgrade compatibility, and monitoring overall instance status. |
| **data**              | execute_sql, list_tables, list_views, list_schemas, list_triggers, list_indexes, list_sequences, list_stored_procedure                                                         | 7     | Use these tools when you need to explore the database structure, discover schema objects like views or stored procedures, and execute custom SQL queries to interact with your data.                      |
| **monitor**           | get_system_metrics, get_query_metrics, list_query_stats, get_query_plan, list_database_stats, list_active_queries, long_running_transactions, list_locks                       | 6     | Use these tools when you need to troubleshoot performance bottlenecks, analyze query execution plans, identify resource-heavy processes, and monitor system-level PromQL metrics.                         |
| **health**            | list_top_bloated_tables, list_invalid_indexes, list_table_stats, get_column_cardinality, list_autovacuum_configurations, list_tablespaces, database_overview, list_pg_settings |       | Use these tools when you need to audit database health, identify storage bloat, find invalid indexes, analyze table statistics, and manage maintenance configurations like autovacuum.                    |
| **view-config**       | list_available_extensions, list_installed_extensions, list_memory_configurations, list_pg_settings, database_overview, get_instance                                            |       | Use these tools when you need to discover and manage PostgreSQL extensions or fine-tune engine-level settings such as memory allocation and server configuration parameters.                              |
| **replication**       | replication_stats, list_replication_slots, list_publication_tables, list_roles, list_pg_settings, database_overview                                                            |       | Use these tools when you need to monitor replication health, manage sync states between nodes, and audit database roles and security settings to ensure environment integrity.                            |

**OneMCP Comparison:**

- **Unique to MCP Toolbox:** Extension management (list_available_extensions) and query plan analysis.
- **Missing in Toolbox:** PostgreSQL lifecycle management (delete_instance, update_instance).

### **Cloud SQL MySQL & Standalone**

| Proposed Toolset Name | Recommended Tools                                                                                                                        | Count | Toolset Description                                                                                                                                                                             |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- | :---- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **admin**             | create_instance get_instance list_instances create_database list_databases create_user wait_for_operation                                | 7     | Use these tools when you need to provision new Cloud SQL for MySQL instances, create databases and users, clone existing environments, and monitor the progress of infrastructure operations.   |
| **data**              | execute_sql, list_tables, get_query_plan, list_active_queries                                                                            | 6     | Use these tools when you need to explore your database schema, execute SQL queries to interact with your data, and inspect how MySQL plans to execute your statements.                          |
| **monitor**           | get_query_plan, list_active_queries, get_query_metrics, get_system_metrics, list_table_fragmentation, list_tables_missing_unique_indexes | 2     | Use these tools when you need to troubleshoot slow queries, analyze system-level PromQL metrics, and identify structural performance issues like table fragmentation or missing unique indexes. |
| **lifecycle**         | create_backup restore_backup clone_instance list_instances wait_for_operation                                                            | 5     | Use these tools when you need to manage the durability and safety of your data by creating backups, restoring from previous states, or cloning instances for recovery and testing.              |

**OneMCP Comparison:**

- **Unique to MCP Toolbox:** Maintenance and observability insights (list_table_fragmentation, get_query_plan).
- **Unique to OneMCP:** Instance lifecycle (delete_instance, update_instance), import_data, export_data, and user management (delete_user).

### **Cloud SQL SQL Server & Standalone**

| Proposed Toolset Name | Recommended Tools                                                                                         | Count | Toolset Description                                                                                                                                                                              |
| :-------------------- | :-------------------------------------------------------------------------------------------------------- | :---- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **admin**             | create_instance get_instance list_instances create_database list_databases create_user wait_for_operation | 7     | Use these tools when you need to provision new Cloud SQL for SQL Server instances, create databases and users, clone existing environments, and monitor the progress of long-running operations. |
| **data**              | execute_sql list_tables                                                                                   | 5     | Use these tools when you need to explore the database schema, execute SQL queries to interact with your data, and monitor system-level performance metrics using PromQL queries.                 |
| **monitor**           | get_system_metrics                                                                                        |       | Use these tools when you need to troubleshoot slow queries and analyze system-level PromQL metrics.                                                                                              |
| **lifecycle**         | create_backup restore_backup clone_instance list_instances wait_for_operation                             | 5     | Use these tools when you need to manage the lifecycle and durability of your data, including creating backups, restoring from existing backups, and cloning instances for testing or migration.  |

**OneMCP Comparison:**

- **Parity:** Core execution and administrative tools are aligned.

### **Looker & Conversational Analytics**

| Proposed Toolset Name | Recommended Tools                                                                                                                                            | Count | Toolset Description                                                                                                                                                                                      |
| :-------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- | :---- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **looker-modeling**   | get_models get_explores get_dimensions get_measures get_filters get_parameters                                                                               | 6     | Handles LookML semantic layer discovery. Use when the user needs to understand what data fields are available for analysis. Provides detailed exploration of dimensions, measures, and model structures. |
| **looker-content**    | get_looks run_look make_look get_dashboards run_dashboard make_dashboard add_dashboard_element add_dashboard_filter                                          | 8     | Manages user-facing BI assets like Looks and Dashboards. Use for creating, searching, or executing saved visualizations. Provides full lifecycle management for reporting content.                       |
| **looker-dev**        | get_projects get_project_files get_project_file create_project_file update_project_file delete_project_file validate_project dev_mode                        | 8     | Focused on the developer workflow and LookML file management. Use for code changes, validation, and project exploration. Provides file-level CRUD operations and syntax checking.                        |
| **looker-ops**        | health_pulse health_analyze health_vacuum get_connections get_connection_schemas get_connection_databases get_connection_tables get_connection_table_columns | 8     | Handles platform maintenance and database connection audits. Use for instance health checks or database schema discovery. Provides connectivity management and LookML cleanup suggestions.               |

**OneMCP Comparison:** Looker is unsupported by OneMCP due to no OP API

###

### **Firestore**

| Proposed Toolset Name  | Recommended Tools                                                                              | Count | Toolset Description                                                                                                                                                             |
| :--------------------- | :--------------------------------------------------------------------------------------------- | :---- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **firestore-data**     | get_documents add_documents update_document delete_documents query_collection list_collections | 6     | Handles NoSQL document operations and collection hierarchy exploration. Use for CRUD tasks and data retrieval. Provides flexible document manipulation and structured querying. |
| **firestore-security** | get_rules validate_rules                                                                       | 2     | Manages access control and security compliance. Use when auditing permissions or deploying new security logic. Provides rule retrieval and syntax validation.                   |

**OneMCP Comparison:**

- **Unique to OneMCP:** Field-level management (field_get, field_update), backup management (backup_get, backup_delete), and schema/insights tools.
- **Missing in Toolbox:** database creation, import_data, export_data, and backup_schedule management.

### **Healthcare API**

No changes required. Already use toolsets.

**OneMCP Comparison:**

- OneMCP does not currently list a specific Healthcare API toolset. MCP Toolbox provides a specialized competitive advantage here.

### **Spanner**

_Includes: GoogleSQL and PostgreSQL dialects._

| Proposed Toolset                       | Recommended Tool Names                                                                                                                                    |
| :------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **spanner-data** (No changes required) | list_tables list_graphs execute_sql execute_dql_sql                                                                                                       |
| **spanner-admin** (Future/Unplanned)   | create_instance get_instance update_instance delete_instance list_instances create_database get_database update_schema drop_database get_operation_status |

**OneMCP Comparison:**

- **Unique to OneMCP:** Session management (create_session, commit).
- **Missing in Toolbox:** Admin/Lifecycle tools

### **Dataplex**

| Proposed Toolset                             | Recommended Tool Names                                              |
| :------------------------------------------- | :------------------------------------------------------------------ |
| **dataplex-discovery** (No changes required) | search_entries lookup_entry search_aspect_types                     |
| **dataplex-quality** (Coming soon)           | get_data_profile get_data_quality run_profile_scan run_quality_scan |

**OneMCP Comparison:**

- **Unique to OneMCP:** get_lineage_graph

## **Additional Work**

### **GitHub PR Check**

We should add a test or a Gemini CLI review for keeping track of toolset sizes.

### **Versioning Policy**

We need to write a versioning guide for toolsets to answer questions like are toolsets changes breaking changes?

## **Appendix**

### **3P Toolsets**

The following toolsets are already compliant with size limits and require no structural changes:

- **ClickHouse**: execute_sql, list_databases, list_tables
- **Elasticsearch**: execute_query
- **Neo4j**: execute_cypher, get_schema
- **Spark**: list_batches, get_batch, cancel_batch, create_pyspark_batch, create_spark_batch
- **SQLite**: execute_sql, list_tables
- **SingleStore / Snowflake / MindsDB / OceanBase**: execute_sql, list_tables

| Current Name        | Recommended Change        | Reason                           |
| :------------------ | :------------------------ | :------------------------------- |
| mindsdb-execute-sql | execute_sql               | Remove redundant prefix.         |
| mindsdb-sql         | execute_parameterized_sql | Remove prefix; increase clarity. |
| execute_esql_query  | execute_query             | Remove engine-specific acronyms. |
| fhir_patient_search | search_patients           | Outcome-oriented naming.         |

### **No MCP Toolbox Support**

#### **Dataform OneMCP**

MCP Toolbox currently supports dataform-compile.

| Proposed Toolset   | Recommended Tool Names                                                               |
| :----------------- | :----------------------------------------------------------------------------------- |
| **dataform-repo**  | create_repository, delete_repository, list_repositories                              |
| **dataform-files** | search_file, rename_file, write_file, delete_file, read_file, list_files_and_folders |
| **dataform-ops**   | compile_pipeline, trigger_pipeline                                                   |

#### **Bigtable OneMCP**

MCP Toolbox currently supports bigtable-sql.

| Proposed Toolset  | Recommended Tool Names                                                      |
| :---------------- | :-------------------------------------------------------------------------- |
| **bigtable-data** | list_instances, get_instance_info, list_tables, get_table_info, execute_sql |

[image1]: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAbCAMAAAC6CgRnAAADAFBMVEX///+5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+a5Q+bLcuzYlvHcofPpxffu0fnGZuvTiu/hrfT79P7///+9T+jlufb26PzPfu7CW+ny3Prn2uy+msydaLKVW6t8NZjfzeb38/mMTqWEQp7OtNmldLitgb/WwN+DN6KLOauaPL+pQNKuQNiePcSHOKd/Np2mP87Gp9KxQdy1QuG2jsWiPsnx5/Xv5vKTOrXt0Pjq0PTmz+/bwuXXtuO2Td7q2/HizurFnNW+kNCoa8CWO7qPOrG4WN3NqdoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACsRY1SAAAAEHRSTlMAEECAoMDQMFCwcJDg8GAggbhKsQAAANBJREFUeF6NkjkOAjEMRR2GYYkbGs7B/S9Dj9yEYmiQELG/s8wMAn6RxHnyEjuBqk7YUr0IcwA5djZDBRpbEJVSZR+QwU1vh7Gkh9ncIraHmykzR05UTlOJmRFzO5u2vmckdKapmlkBIaNHcoqozS+Od6KZL/JZ6U/LI8KlW2AXWymCstuIeQRjJJpo17GbLodBzKgvBbvq8xYk58M4WEtU0qHSFzGHnlCbA6+IMgSV2s2ipLUka5t25DX4/d5m+23uv/4LrShq+ON/qhw7yHoD2LYrfWJ+HeEAAAAASUVORK5CYII=

# databricks-analyst-study-notes
Databricks Data Analyst Associate Study Notes

## Section 1 – Databricks SQL

### Audience and Usage
- **Primary audience**: Data analysts who query and visualize data using Databricks SQL.
- **Side audiences**: Business users, engineers, and data scientists consuming dashboards.
- Dashboards can be viewed and run by a broad range of stakeholders.

### Advantages of Using Databricks SQL
- Enables **in-Lakehouse querying**, avoiding data movement to third-party tools.
- Streamlines BI workflows and simplifies data access across roles.
- Ideal for exploratory analysis, dashboarding, and embedded analytics.

### Querying in Databricks SQL
- SQL is written and executed inside the **Query Editor**.
- The **Schema Browser** helps explore available databases, tables, columns, and data types.
- Supports all standard SQL operations: `SELECT`, `JOIN`, `WHERE`, `GROUP BY`, etc.

### Dashboards
- **Databricks SQL dashboards** aggregate the output of multiple queries into a single interface.
- Dashboards can be built by selecting visualizations for individual query outputs.
- Dashboards support **scheduled auto-refresh** to stay current with underlying data.

### SQL Endpoints / Warehouses vs. Clusters

#### SQL Endpoints (Warehouses)
- Purpose-built for **BI tools**, dashboards, and SQL queries.
- Support **partner integrations** like Fivetran, Tableau, Power BI, and Looker.
- **Serverless endpoints** are ideal for fast, low-maintenance access.
- Choose based on **concurrency and SLA needs**—larger endpoints cost more but handle more load.

#### Clusters
- Used for **notebooks**, **data engineering**, **ETL**, and **interactive Spark jobs**.
- Provide full flexibility, including support for non-SQL workloads (e.g., Python, Scala).
- Not used directly for dashboards or SQL endpoints.

### Data Integration and Ingestion
- **Partner Connect** simplifies integration with tools like Fivetran, requiring partner-side setup.
- **Small-file upload** supports importing files like CSVs for quick testing or lookups.
- Supports ingesting data from **object storage** (S3, ADLS) including **directories of files** of the same type.

### Visualization Tool Integration
- Native connectors available for Tableau, Power BI, and Looker.
- Databricks SQL complements these tools by serving as a **fast, scalable backend**.
- Can be used to manage transformations and deliver clean tables for visual consumption.

### Medallion Architecture
- Data is structured into **bronze (raw)**, **silver (cleaned)**, and **gold (aggregated)** layers.
- **Gold layer** is most relevant to analysts and dashboards.
- Promotes clarity, reliability, and reusability of datasets across teams.

### Streaming Data
- The **Lakehouse architecture** supports combining **batch and streaming data**.
- **Benefits**: Enables real-time dashboards and timely alerting.
- **Cautions**:
  - Streaming requires proper handling of data latency and order.
  - More complex to design and maintain than batch pipelines.

## Section 2 – Data Management

### Delta Lake Overview
- **Delta Lake** is a storage layer that provides ACID transactions, scalable metadata handling, and unified batch/streaming data processing.
- Manages **table metadata** (schema, versions, history) automatically.
- Maintains **history of table changes**, enabling time travel and rollback features.

### Benefits of Delta Lake in the Lakehouse
- Combines the reliability of data warehouses with the scalability of data lakes.
- Supports schema enforcement and evolution, making it easier to work with changing data.
- Enables efficient reads and writes through data versioning and indexing.

### Table Persistence and Scope
- Tables in Databricks can be **managed** or **unmanaged**:
  - **Managed tables**: Databricks manages both metadata and data location.
  - **Unmanaged tables**: Only metadata is managed; data lives in external storage.
- Use the `LOCATION` keyword to specify a custom path for table data when creating a database or table.

### Managed vs. Unmanaged Tables
- **Managed**:
  - Data is deleted when the table or database is dropped.
  - Stored in the workspace-managed location.
- **Unmanaged**:
  - Data remains in place even if the table is dropped.
  - Suitable for shared storage or external ingestion pipelines.
- Use metadata inspection or tools like **Data Explorer** to determine table type.

### Creating and Managing Database Objects
- Use SQL commands or UI to:
  - `CREATE`, `DROP`, and `RENAME` **databases**, **tables**, and **views**.
- Databricks supports:
  - **Permanent views**: Logical definitions that reference underlying tables.
  - **Temporary views (temp views)**: Exist only for the session, not persisted to the metastore.

### Views vs. Temp Views
- **Views**:
  - Persist across sessions.
  - Accessible by all users with appropriate permissions.
- **Temp views**:
  - Exist only for the session and user that created them.
  - Useful for ad hoc or intermediate queries.

### Data Explorer Capabilities
- Used to:
  - **Explore**, **preview**, and **secure** data.
  - Identify the **owner of a table**.
  - Change **access permissions** for users and groups.
- Supports **access control** via Unity Catalog (where available) or workspace-level permissions.

### Access Management
- **Table owners** have full privileges to manage table metadata and data.
- Responsibilities include managing access, updating schemas, and sharing data appropriately.
- Use **Data Explorer** or SQL commands to grant/revoke privileges.

### PII and Organizational Considerations
- Personal Identifiable Information (PII) must be handled according to **organizational policies**.
- Data analysts should be aware of:
  - Data classification and masking policies.
  - Access control rules for sensitive data.
  - Audit and compliance requirements tied to PII usage.


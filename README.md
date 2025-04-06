# Databricks Certified Data Analyst Associate – Study Notes

These are condensed study notes for the **Databricks Certified Data Analyst Associate** exam, based on the official [exam guide (Mar 1, 2025 version)](https://www.databricks.com/learn/certification/databricks-certified-data-analyst-associate).

## Exam Overview
- **Format**: 45 multiple-choice questions
- **Duration**: 90 minutes
- **Delivery**: Online proctored exam
- **Prerequisites**: None officially required, but 6+ months hands-on Databricks experience is recommended
- **Scope**: Focuses on using Databricks SQL to perform data analysis, build dashboards, manage Lakehouse data, and integrate with BI tools


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

## Section 3 – SQL in the Lakehouse

### Querying Fundamentals
- Identify queries that retrieve data using `SELECT` with specific `WHERE` conditions.
- Understand and interpret the **output of a SELECT query** based on its columns and clauses.

### Data Insertion and Merging
- Know when to use:
  - `MERGE INTO`: For upserts (insert/update based on match conditions).
  - `INSERT INTO`: To append new rows into a table.
  - `COPY INTO`: For loading external files (e.g., CSV, JSON, Parquet) into Delta tables.

### Query Simplification
- Use **subqueries** (nested SELECTs) to simplify complex queries and improve modularity.

### Joins
- Compare and contrast different types of joins:
  - `INNER JOIN`: Only matching records from both sides.
  - `LEFT OUTER JOIN`: All records from the left, and matched ones from the right.
  - `RIGHT OUTER JOIN`: All records from the right, and matched ones from the left.
  - `FULL OUTER JOIN`: All records when there is a match in either left or right.
  - `CROSS JOIN`: Cartesian product of both tables (all combinations).

### Aggregations
- Use aggregate functions like `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()` to produce summary metrics.
- Group results using `GROUP BY` to structure the output.

### Nested Data
- Handle **nested data formats** (like structs or arrays) using dot notation and functions like `explode()`.

### Cube and Roll-Up
- Use `ROLLUP` to aggregate hierarchically from the most detailed to the grand total.
- Use `CUBE` to compute all combinations of groupings.
- Know the difference:
  - **ROLLUP** is hierarchical and includes subtotals.
  - **CUBE** includes all possible subtotal combinations.

### Window Functions
- Use **windowing** (analytic) functions to calculate metrics across time or partitions:
  - Examples: `ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`, `SUM() OVER (...)`.

### ANSI SQL Benefits
- Having **ANSI SQL support** ensures consistency, portability, and familiarity.
- Reduces the learning curve and enables analysts to apply standard SQL practices.

### Silver-Level Data
- **Silver data** is cleaned and joined, ready for consumption or further enrichment.
- Know how to **identify**, **access**, and **clean** silver-layer data for analysis.

### Query Optimization
- Use **query history** to review and improve past queries.
- **Caching** frequently used datasets or results helps reduce query latency and development time.

### Spark SQL Performance Tuning
- Use **higher-order functions** (e.g., `transform`, `filter`, `aggregate`) for more efficient operations on arrays and maps.
- Optimize queries for performance using these functional programming-like constructs.

### User-Defined Functions (UDFs)
- Create and apply **UDFs** when built-in SQL functions are insufficient.
- UDFs allow for reusable custom logic in common or complex transformations.
- Understand appropriate scenarios for UDFs, especially when scaling across large datasets.

## Section 4 – Data Visualization and Dashboarding

### Creating Visualizations
- Build **basic visualizations** directly from query results in Databricks SQL.
- Visualizations are **schema-specific** (based on query output structure).
- Supported visualization types include:
  - **Table**
  - **Details**
  - **Counter**
  - **Pivot table**

### Formatting and Storytelling
- Visualization formatting significantly impacts **how insights are perceived**.
- Enhance clarity and impact through:
  - Proper labeling
  - Axis scaling
  - Color usage
  - Consistent formatting
- Use formatting techniques to **add visual appeal** and guide interpretation.
- Customize visualizations to support **data storytelling**, emphasizing key trends or comparisons.

### Dashboard Composition
- Build dashboards by combining **multiple existing visualizations** from saved Databricks SQL queries.
- Adjust **color schemes across visualizations** for a consistent appearance.
- Use **query parameters** to allow dynamic updates to dashboard content based on user input.

### Dashboard Parameters
- Understand how **parameters** affect the underlying query output:
  - Example: A dropdown that filters data by region or date.
- Use **"Query-Based Dropdown List"** to populate a parameter from the distinct results of another query.
- This enables dynamic, user-driven filtering across visualizations.

### Dashboard Sharing and Refreshing
- Share dashboards in multiple ways:
  - With edit or view access
  - Public or private links (workspace dependent)
- Evaluate **pros and cons** of each sharing method:
  - Public links are easy to distribute but reduce control.
  - Private dashboards maintain control but require user access setup.

### Credential Behavior
- Dashboards can be **refreshed using the owner's credentials**, allowing access for users without direct permissions to all underlying objects.
- This supports safe and controlled dashboard sharing.

### Refresh Scheduling
- Configure **automatic refresh intervals** to keep dashboards updated.
- Be aware of potential issues:
  - If a dashboard’s refresh rate is **shorter than the warehouse's Auto Stop setting**, the warehouse may shut down before a refresh occurs.
  - Consider aligning refresh schedules with warehouse lifecycle settings.

### Alerts
- Alerts monitor the **result of a query** and trigger **notifications** when a specified condition is met.
- Use cases include monitoring thresholds, anomalies, or status flags (e.g., "value exceeds 100", "row count is zero").
- Alerts are configured by:
  - Selecting a saved query
  - Defining a condition (e.g., `value > X`)
  - Choosing a target column and row (if applicable)
  - Specifying one or more notification channels (email, webhook, Slack, etc.)

#### Key Limitations
- **Alerts only work on queries that return a single numeric value** (e.g., row count, sum, or a calculated metric).
- Alerts **do not work with queries that return multiple rows or complex result sets**.
- Alerts are **not compatible with date-type query parameters**.
- Alerts **only support dropdown-based query parameters**—these can be static lists or populated from a query.
  - For example, you can filter by region or category using a dropdown, but you cannot pass in a date picker.

#### Best Practices
- Use alerts on queries specifically designed to return a single value for evaluation.
- Avoid complex aggregations or queries with joins unless they simplify to a single numeric result.
- Use parameterized queries with dropdowns for dynamic alerting across categories (e.g., per region or per status).
- Align alert check frequency with your dashboard/warehouse refresh schedules.

## Section 5 – Analytics Applications

### Statistics and Distributions
- **Discrete statistics** involve countable values (e.g., number of transactions).
- **Continuous statistics** involve measurable quantities on a continuum (e.g., temperature, revenue).
- Understand and apply **descriptive statistics**:
  - Measures of central tendency: mean, median, mode
  - Measures of dispersion: variance, standard deviation, range

- Identify and interpret **key moments** of statistical distributions:
  - **1st moment (Mean)** – central value
  - **2nd moment (Variance/Standard Deviation)** – spread of data
  - **3rd moment (Skewness)** – asymmetry of the distribution
  - **4th moment (Kurtosis)** – "tailedness" or outlier sensitivity

- Compare and contrast common **statistical measures**:
  - Mean vs. median (sensitivity to outliers)
  - Standard deviation vs. interquartile range

### Data Enhancement
- **Data enhancement** refers to enriching existing datasets by adding new attributes, calculations, or contextual information.
- This is a common step in analytics workflows to improve model accuracy or business relevance.
- Examples include:
  - Adding demographic features
  - Calculating customer lifetime value
  - Generating derived fields (e.g., revenue per user)

- Identify scenarios where **data enhancement** is beneficial:
  - Improving dashboard insights
  - Supporting more granular segmentation
  - Enabling better forecasting or prediction

### Data Blending
- **Data blending** involves combining data from **two or more source applications**.
- Typically used when joining internal and external datasets that are not in the same system.
- Scenarios where blending is useful:
  - Merging CRM data with support ticket logs
  - Joining product data from an ERP with marketing campaign performance

### Last-Mile ETL
- **Last-mile ETL** refers to project-specific transformations performed near the end of a data pipeline.
- Often involves:
  - Cleaning or reshaping gold-layer data
  - Formatting results for a specific dashboard or report
  - Applying business rules or mappings for final delivery

- Supports the specific analytical needs of a team, stakeholder, or use case.


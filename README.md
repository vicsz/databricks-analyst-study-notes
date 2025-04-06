# Databricks Certified Data Analyst Associate – Study Notes

These are condensed study notes for the **Databricks Certified Data Analyst Associate** exam, based on the official [exam guide (Mar 1, 2025 version)](https://www.databricks.com/learn/certification/databricks-certified-data-analyst-associate).

## Study Notes: Exam Insights

### Overall Difficulty and Format
- The exam is **entry-level**, targeting data analysts comfortable with SQL and basic analytics tasks.
- Considered **easier than Data Engineer Associate** and **more practical than theory-heavy**.
- **45 multiple-choice questions** in **90 minutes** — generous time allowance.
- Candidates with solid SQL knowledge and light Databricks familiarity often pass with **minimal prep**.

---

## Key Topics to Understand (with Details)

## Databricks SQL Interface & Dashboarding

### SQL Editor
- The **SQL Editor** allows users to write, run, and save SQL queries.
- Features include:
  - **Schema browser** to explore available tables and columns.
  - **Query results** can be visualized (e.g., bar charts, line charts, pivot tables).
  - Queries can be **scheduled** to run at regular intervals or to **trigger alerts**.

### Dashboards
- Dashboards are built by **adding visualizations** based on one or more queries.
- A **single query** can have **multiple visualizations**, and all can be added to the same dashboard.
- Visualizations can include filters or **parameters** to allow **interactive control** for dashboard users.

### Parameters and Dashboard Interactivity
- You can assign **query parameters** to a **Dashboard Parameter**.
- This links that parameter across multiple visualizations so they **stay in sync** when the user changes the value on the dashboard.
- This is useful for filtering all visuals (e.g., by region or product) using a single dropdown control.

### Sharing Dashboards Securely
- Dashboards can be shared **without granting access to the underlying data or workspace** using:
  - **PDF export**
  - **PNG export of visualizations**
  - **Screenshots**
  - **Email subscriptions** (via refresh schedule with recipients added)
- **Do not** share **Personal Access Tokens (PATs)**. These provide full authenticated access and violate security requirements.

### Visualization Types

| Visualization       | What It Is                                             | When to Use                                                                                   |
|---------------------|--------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Bar Chart**        | Vertical bars comparing values                        | Compare values across categories (e.g., sales by region, product types)                       |
| **IBar Chart**       | Inline-style bar chart                                | Use in compact dashboards with limited space                                                  |
| **Line Chart**       | Line connecting data points                           | Show trends over time (e.g., revenue over months)                                             |
| **Area Chart**       | Line chart with filled area                           | Emphasize total volume or magnitude over time                                                 |
| **Pie Chart**        | Circle divided into segments                          | Show part-to-whole relationships with few categories (ideally less than 5)                    |
| **Histogram**        | Distribution chart                                    | Show frequency distribution of a numeric variable (e.g., age, purchase size)                  |
| **Scatter Plot**     | Plot of two numeric axes                              | Show relationships or correlations between two numeric variables                              |
| **Heatmap**          | Grid of values with color shading                     | Display intensity across two categorical dimensions (e.g., hour of day vs. day of week)       |
| **Pivot Table**      | Table with groupings and aggregation                  | Summarize and drill into data by multiple dimensions                                          |
| **Counter**          | Large number representing a metric                    | Display a single key metric (e.g., daily active users)                                        |
| **Sankey**           | Flow diagram with weighted connections                | Visualize paths or flows (e.g., user journey through a website)                               |
| **Word Cloud**       | Words sized by frequency                              | Show frequency of terms (e.g., top search queries)                                            |
| **Choropleth Map**   | Map with shaded regions                               | Show geographic distribution (e.g., sales by country or state)                                |

### SQL and Advanced Querying in Databricks

#### Window Functions
- Allow you to perform **row-wise calculations across partitions** of data (like moving averages or rankings).
- Example:
  ```sql
  SELECT name, region, revenue,
         RANK() OVER (PARTITION BY region ORDER BY revenue DESC) AS rank
  FROM sales;
  ```
- Common window functions: `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `LAG()`, `LEAD()`, `SUM() OVER(...)`

#### Aggregations
- Know how to use `GROUP BY` with functions like `COUNT()`, `AVG()`, `MIN()`, `MAX()`, `SUM()`.
- Understand differences between **scalar aggregation** and **group-level aggregation**.

#### Subqueries
- Queries nested inside `SELECT`, `FROM`, or `WHERE`.
- Useful for filtering or isolating logic in complex queries.

#### Higher-Order Functions (Spark SQL Extensions)
- Useful when working with arrays, maps, or nested fields.
- Examples: `transform`, `filter`, `exists`, `aggregate`
  ```sql
  SELECT transform(array(1, 2, 3), x -> x + 1);
  -- returns [2, 3, 4]
  ```

---

### Delta Lake & Table Management

#### Table Types
- **Managed Tables**: Databricks stores both metadata and data; dropped table = data deletion.
- **Unmanaged Tables**: External data location; only metadata is deleted if table is dropped.

#### Delta Lake Features
- Delta Lake is Databricks' transaction layer on top of Parquet:
  - **ACID Transactions**: Ensures consistency.
  - **Time Travel**: Query older versions using `VERSION AS OF` or `TIMESTAMP AS OF`.
  - **Schema Enforcement**: Ensures data types match expectations.
  - **Schema Evolution**: Controlled changes to schema (with permissions).
  
- Know key operations:
  - `OPTIMIZE` – Compacts small files into larger ones to improve read performance.
  - `ZORDER BY` – Reorders data to improve performance on selective queries (similar to indexing).
  - `MERGE INTO` – Performs upserts (insert/update) into a Delta table based on conditions.

---

### Visualization and Interactive Analytics
- Visualization types supported:
  - **Table**, **Counter**, **Pivot**, **Bar/Line charts**
- Visualizations are tied to **query results**, and can be reused across dashboards.
- You can **format** visuals for readability (e.g., number precision, axis scaling).
- **Query parameters** can drive dynamic filters, but only **dropdowns** are supported in alerts.

---

### Alerts and Scheduling
- **Alerts** trigger when a query returns a value that meets a specified condition.
  - Example: Trigger an email if sales fall below $10,000.
- Must be based on **single-value numeric queries** (e.g., `SELECT COUNT(*)`).
- Only **dropdown parameters** are supported — **date pickers do not work** with alerts.
- Alerts can **notify via email or webhook** and are configured from the UI.
- **Query Scheduling**:
  - Queries or dashboards can be set to auto-refresh at intervals.
  - Important: Ensure the warehouse used doesn't shut down before the refresh triggers (align auto-stop and schedule).

---

### Partner Connect and BI Integration

- **Partner Connect** enables quick, UI-based connections to:
  - **BI tools**: Tableau, Power BI, Looker
  - **Ingestion tools**: Fivetran, Rivery, dbt
- Reduces setup time and removes the need for manual config.
- Also supports small file uploads (CSV) and external database connections (via federation).

---

### Security and Governance (Basic Analyst-Level)

- Analysts can manage:
  - **Sharing queries/dashboards**
  - **Transferring ownership** of artifacts (e.g., if a colleague leaves).
- Databricks supports **fine-grained access control**:
  - **Viewers** can refresh dashboards (if using owner’s credentials).
  - **Editors** can update or modify queries and visuals.
- Know the difference between **table/view/query access vs. dashboard-level sharing**.

---


# Databricks SQL Language Study Guide

---

## DDL – Data Definition Language

### Create Tables
```sql
CREATE TABLE sales (
  id INT,
  region STRING,
  amount DOUBLE
);
```
- Creates a managed table stored by Databricks.
- To create an external (unmanaged) table, use the `LOCATION` clause.

```sql
CREATE TABLE external_sales (
  id INT,
  region STRING,
  amount DOUBLE
)
USING DELTA
LOCATION '/mnt/data/external_sales/';
```

### Drop and Rename Tables
```sql
DROP TABLE IF EXISTS sales;
ALTER TABLE sales RENAME TO sales_2024;
```

---

## DML – Data Manipulation Language

### Insert, Update, Delete
```sql
INSERT INTO sales VALUES (1, 'East', 100.0);

UPDATE sales SET amount = amount * 1.1 WHERE region = 'East';

DELETE FROM sales WHERE region = 'West';
```

---

## Views and Temporary Views

### Permanent Views
Stored in the metastore and accessible across sessions.
```sql
CREATE OR REPLACE VIEW top_regions AS
SELECT region, SUM(amount) AS total FROM sales GROUP BY region;
```

### Temporary Views
Session-scoped. Ideal for intermediate results or testing.
```sql
CREATE OR REPLACE TEMP VIEW temp_sales AS
SELECT * FROM sales WHERE amount > 100;
```

---

## Temporary Tables (via Views)

Databricks supports temp views instead of temp tables. Use temp views to simulate session-local temporary tables:
```sql
CREATE OR REPLACE TEMP VIEW temp_table AS
SELECT * FROM sales WHERE amount > 100;
```

---

## Subqueries and CTEs

### Subqueries
Used to filter or derive values inside another query.
```sql
SELECT * FROM sales
WHERE region IN (SELECT region FROM blacklist);
```

### Common Table Expressions (CTEs)
Named, reusable subqueries defined with `WITH`. Good for readability and modular SQL logic.
```sql
WITH high_sales AS (
  SELECT region, SUM(amount) AS total
  FROM sales
  GROUP BY region
  HAVING total > 1000
)
SELECT * FROM high_sales;
```

---

## Joins (Standard and Extended)

| Join Type        | Description                                                  |
|------------------|--------------------------------------------------------------|
| INNER JOIN       | Matches rows in both tables                                  |
| LEFT OUTER JOIN  | All rows from left + matched rows from right                |
| RIGHT OUTER JOIN | All rows from right + matched rows from left                |
| FULL OUTER JOIN  | All rows from both sides                                     |
| CROSS JOIN       | All possible combinations                                    |
| LEFT SEMI JOIN   | Keeps left-side rows with matches in right (like a filter)   |
| LEFT ANTI JOIN   | Keeps left-side rows **without** matches in right            |

### ANTI JOIN Example
```sql
SELECT * FROM sales
LEFT ANTI JOIN blacklist ON sales.region = blacklist.region;
```
Returns only sales rows where region is NOT in the blacklist.

---

## Window Functions

Enable ranking, row-wise calculations, and running totals within partitions of data.

```sql
SELECT id, region, amount,
       RANK() OVER (PARTITION BY region ORDER BY amount DESC) AS rank
FROM sales;
```

Common window functions:
- `ROW_NUMBER()`
- `RANK()`, `DENSE_RANK()`
- `LAG()`, `LEAD()`
- `SUM() OVER (...)`

---


## CUBE and ROLLUP

### Input Table: `sales`

| region | product | amount |
|--------|---------|--------|
| East   | A       | 100    |
| East   | B       | 200    |
| West   | A       | 150    |
| West   | B       | 150    |

---

### ROLLUP

The `ROLLUP` operator creates subtotals that **roll up** from the most granular level to a grand total, following the column order.

```sql
SELECT region, product, SUM(amount) AS total_sales
FROM sales
GROUP BY ROLLUP(region, product);
```
or
```sql
SELECT region, product, SUM(amount) AS total_sales
FROM sales
GROUP BY region, product WITH ROLLUP;
```

#### Explanation:
- Subtotals are calculated in a **hierarchical** manner.
- Aggregation moves from `(region, product)` → `(region)` → `()` (grand total).

#### ROLLUP Output

| region | product | total_sales |
|--------|---------|-------------|
| East   | A       | 100         |
| East   | B       | 200         |
| East   | NULL    | 300         |
| West   | A       | 150         |
| West   | B       | 150         |
| West   | NULL    | 300         |
| NULL   | NULL    | 600         |

---

### CUBE

The `CUBE` operator generates **all combinations** of the specified grouping columns, including subtotals across each dimension and the grand total.

```sql
SELECT region, product, SUM(amount) AS total_sales
FROM sales
GROUP BY CUBE(region, product);
```
or
```sql
SELECT region, product, SUM(amount) AS total_sales
FROM sales
GROUP region, product WITH CUBE;
```

#### Explanation:
- Returns subtotals for:
  - `(region, product)`
  - `(region)`
  - `(product)`
  - `()` (grand total)
- Useful for multi-dimensional analysis and pivot-style reporting.

#### CUBE Output

| region | product | total_sales |
|--------|---------|-------------|
| East   | A       | 100         |
| East   | B       | 200         |
| East   | NULL    | 300         |
| West   | A       | 150         |
| West   | B       | 150         |
| West   | NULL    | 300         |
| NULL   | A       | 250         |
| NULL   | B       | 350         |
| NULL   | NULL    | 600         |

---

### Summary

- Use ROLLUP when you want hierarchical subtotals, moving from detailed to summary levels (e.g., region → total). Returns fewer rows with only valid rollup paths.
- Use CUBE when you want all possible subtotals across every grouping combination (like a pivot table). Returns more rows including all subtotal combinations.

---

## Delta Lake Features

### MERGE INTO (Upserts)
Performs update or insert based on match condition.
```sql
MERGE INTO target USING source
ON target.id = source.id
WHEN MATCHED THEN
  UPDATE SET amount = source.amount
WHEN NOT MATCHED THEN
  INSERT (id, region, amount) VALUES (source.id, source.region, source.amount);
```

### OPTIMIZE
Combines many small files into larger ones to improve query performance.
```sql
OPTIMIZE sales;
```

### ZORDER
Sorts data to accelerate queries that filter on specific columns.
```sql
OPTIMIZE sales ZORDER BY (region);
```

---

## Higher-Order and Array Functions

Databricks supports advanced functional programming-like syntax.

### EXPLODE (unnest arrays into rows)
```sql
SELECT id, explode(items) AS item
FROM orders;
```

### TRANSFORM (map over array)
```sql
SELECT transform(array(1, 2, 3), x -> x + 1);
-- Result: [2, 3, 4]
```

Other useful functions:
- `FILTER`, `AGGREGATE`, `EXISTS`
- `ARRAY_CONTAINS`, `SIZE`, `MAP_KEYS`

## Inspecting Table Metadata

### DESCRIBE and DESCRIBE EXTENDED

Use `DESCRIBE` to view a table or view’s column structure (name, type, and comment).

```sql
DESCRIBE sales;
```

Use `DESCRIBE EXTENDED` to retrieve both schema information **and** detailed metadata such as:
- Table location
- Provider (e.g., Delta)
- Table type (Managed/External)
- Storage details

```sql
DESCRIBE EXTENDED sales;
```

### Sample Output (DESCRIBE)

| col_name | data_type | comment |
|----------|-----------|---------|
| id       | int       |         |
| region   | string    |         |
| amount   | double    |         |

### Sample Output (DESCRIBE EXTENDED excerpt)

After the schema rows, you’ll also see:

| col_name                   | data_type                                            | comment |
|---------------------------|------------------------------------------------------|---------|
| # Detailed Table Information |                                                      |         |
| Location                  | dbfs:/user/hive/warehouse/sales                      |         |
| Provider                  | delta                                                |         |
| Table Type                | MANAGED                                              |         |
| ...                       | ...                                                  |         |

### Rule of Thumb

- Use `DESCRIBE` to check **schema** quickly.
- Use `DESCRIBE EXTENDED` when you need to confirm **storage details**, **table type**, or **format** (especially for Delta tables).


---


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
- Purpose-built for **SQL queries**, **dashboards**, and **BI tool integrations**.
- Support **Partner Connect integrations** with tools like **Fivetran**, **Tableau**, **Power BI**, and **Looker**.
- Typically the **recommended destination** for tools like Fivetran, which use SQL to ingest or visualize data.
- **Serverless SQL warehouses** offer fast startup, cost efficiency, and are easy to manage.
- Choose based on **concurrency** and **performance needs**—larger or multi-cluster endpoints support higher workloads but at higher cost.

#### Clusters
- Used for **notebooks**, **ETL jobs**, **data engineering**, and **interactive Spark workloads**.
- Support **Python**, **Scala**, **R**, and **SQL** in a more general-purpose environment.
- While **some integrations (like Fivetran) allow clusters as a destination**, Databricks **recommends SQL warehouses** for most partner workflows due to better support for SQL-based access.
- Clusters are not typically used directly for powering dashboards or BI tools.

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
## Statistics and Distributions
---

### Types of Variables

- **Discrete variables**: Represent **countable values**, such as number of transactions or logins. Typically whole numbers.
- **Continuous variables**: Represent **measurable values** on a continuum, such as temperature, revenue, or time. Can take on infinitely fine values.

---

### Descriptive vs. Inferential Statistics

- **Descriptive statistics**: Focus on **summarizing and describing** a dataset using numerical metrics and visualizations.
  - Do not attempt to draw conclusions beyond the data.
  - Example: Calculating the average order value from a dataset.

- **Inferential statistics**: Use sample data to **infer or generalize** about a population.
  - Includes hypothesis testing, confidence intervals, and regression.
  - Not heavily tested on the Databricks exam.

#### Rule of Thumb:
> If it summarizes data without making predictions, it's **descriptive statistics**.

---

### Measures in Descriptive Statistics
#### Central Tendency:
- **Mean**: Average value.
- **Median**: Middle value (less sensitive to outliers).
- **Mode**: Most frequently occurring value.

#### Dispersion:
- **Standard deviation**: How much values deviate from the mean.
- **Variance**: Square of standard deviation.
- **Range**: Difference between max and min.
- **Interquartile range (IQR)**: Spread of the middle 50% of the data (Q3 − Q1).

---

### Moments of a Distribution

| Moment       | What It Describes                        | Use Case Example                                   |
|--------------|-------------------------------------------|----------------------------------------------------|
| **1st**      | Mean – central location                   | Overall average                                    |
| **2nd**      | Variance/Standard Deviation – spread      | How tightly values cluster around the mean         |
| **3rd**      | Skewness – asymmetry                      | Detecting left/right tilt in data distribution     |
| **4th**      | Kurtosis – tail weight and outlier risk   | High kurtosis = heavy tails, more extreme values   |

#### Kurtosis Explained:
- **Low kurtosis**: Data have light tails; few outliers.
- **High kurtosis**: Data have heavy tails; more prone to **extreme values or outliers**.
- Kurtosis is about the **"tailedness"** of a distribution, not its peak.
- Kurtosis measures how likely a distribution is to produce outliers — not how tall or flat the peak is. Think: "How fat are the tails?"

---

### Comparing Statistical Measures

| Concept               | Description and Comparison                                      |
|-----------------------|------------------------------------------------------------------|
| **Mean vs. Median**    | Mean is affected by outliers; median is more robust.            |
| **Standard Deviation vs. IQR** | SD uses all values; IQR focuses on the middle 50% (less sensitive to outliers). |

---

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


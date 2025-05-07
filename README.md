# SQL_Data-Warehousing_Data-Engineering
A Data Warehouse (DW) is used to store, organize, and analyze large volumes of data from multiple sources. It’s optimized for analytics, reporting, and business intelligence (BI) , not for handling day-to-day operations like a transactional database (OLTP).
### Key Reasons We Use a Data Warehouse
Centralized Data from Multiple Sources
A DW integrates data from various systems , like ERP, CRM, APIs, flat files — into a single, consistent format.
### Designed for Fast Queries (OLAP)
Data warehouses are optimized for read-heavy, analytical queries (e.g., trends, aggregations, dashboards), unlike OLTP systems which are optimized for write-heavy workloads.
### Historical Data Storage
You can store years of historical data in a DW, allowing time-based trend analysis, forecasting, and strategic planning.
### Data Quality and Cleansing
During the ETL/ELT process (Extract, Transform, Load), data is cleaned and standardized, which improves reliability for decision-making.
### Support for BI Tools
Tools like Power BI, Tableau, Looker, and others work efficiently with DWs for dashboards and reports.
### Separation of Concerns
Keeps reporting/analytics workloads separate from operational databases, improving performance and stability on both sides.
### Tech Stack Examples
ETL/ELT tools: dbt, Apache Airflow, Fivetran, Informatica

Data Warehouses: Snowflake, Amazon Redshift, Google BigQuery, Azure Synapse, PostgreSQL (for smaller setups)

SQL: Core language for querying and transforming DW data
## What is ETL?
ETL stands for Extract, Transform, Load — it's a core process in data warehousing used to move data from various sources into a centralized data warehouse.

### Extract
Pull data from different sources — databases (like MySQL, Oracle), files (CSV, JSON), APIs, CRMs, etc.
Example: Pull daily sales records from a POS system.

### Transform
Clean, filter, join, or reformat the data.
Common steps:
Fix missing or incorrect values
Convert data types (e.g., text to date)
Join multiple datasets
Aggregate or summarize data
Example: Convert "2025-05-07" to "May 2025" or calculate total monthly sales.

### Load
Store the transformed data into the data warehouse in a structured format.
This could mean loading into tables designed for analytics (like star or snowflake schemas).

## 🟡 Extract Techniques
Goal: Pull data from various source systems.

Methods:
Full Extraction: Load all data every time (simple but slow).
Incremental Extraction: Only extract new or changed data using:Timestamps (e.g., last_updated > '2025-05-06'), Change Data Capture (CDC) from logs or triggers, Versioning or surrogate keys

Tools:
SQL queries, APIs (REST/GraphQL), File ingestion (CSV, Excel, JSON, XML), ETL tools: Fivetran, Talend, Apache NiFi

## 🟠 Transform Techniques
Goal: Clean, format, and reshape the data.

Methods:
Data Cleaning: Remove duplicates, fix nulls, correct types
Standardization: Rename columns, unify date formats, currency, etc.
Filtering: Remove irrelevant rows or outliers
Joins/Merges: Combine datasets from different sources
Aggregations: Sum, count, average, etc., for metrics
Data Enrichment: Add calculated columns or lookup values

Tools:
SQL (CTEs, window functions), dbt (data build tool), Python (Pandas), Spark, Enterprise ETL tools (Informatica, SSIS)

## 🔵 Load Techniques
Goal: Push data into the data warehouse.

Methods:
Full Load: Truncate and reload everything (rare in big data), upsert, drop and create and insert
Incremental Load: Insert only new/updated rows
UPSERT (INSERT + UPDATE)
MERGE statements and append

Batch Load: Load data in scheduled batches (e.g., nightly)
Streaming Load: Load real-time data continuously

Tools:
SQL (INSERT, MERGE, COPY, LOAD DATA), Snowflake, BigQuery, Redshift loaders, Apache Kafka (for streaming), Airflow (orchestrates ETL pipelines)
### Slowly Changing Dimension(SCD):
SCD 0(no historization: nothing should be changed at all)
SCD 1(overwrite: update the records with the new information by resources and overwriting the old values like upsert, but you are loosing the history)
SCD 2(historization: we insert new record for each changes from the sources and we are not delete or overwrite the old data)
SCD 3


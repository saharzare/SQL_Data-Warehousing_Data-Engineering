# SQL_Data-Warehousing_Data-Engineering
### The techniques and types in our project:
Pull & Full Extraction >> with the technique of parsing files to the datawarehouse >> Data Transformation with all  >> Batch & Full(truncate and insert) Load and historization of SCD1
## download the materials
🔗https://datawithbaraa.substack.com
🔗https://datawithbaraa.substack.com/p/build-a-data-warehouse-from-scratch
🔗https://datawithbaraa.substack.com/p/access-to-course-materials
## Which tools important to have?
SSMS,Notion,drawio

## 📊 Project Requirements: 
### 1- Building the Data Warehouse (Data Engineering)
### 🎯 Objective
Design and implement a modern data warehouse using SQL Server to consolidate and prepare sales data for analytical reporting and data-driven decision-making.

📋 Specifications
Data Source: Integrate data from two distinct systems: an ERP and a CRM, both provided in CSV format.
Data Quality: Perform data cleansing and standardization to resolve inconsistencies, missing values, and quality issues before loading.
Integration & Modeling: Merge the ERP and CRM data into a single, unified data model optimized for analytical queries (e.g., star or snowflake schema).
Ensure the model is intuitive and accessible for both technical and non-technical users.
Scope: Focus exclusively on the most recent dataset.
No historization or slowly changing dimension (SCD) tracking is required.
Documentation: Deliver comprehensive documentation of the data model and ETL process.
Ensure clarity for both business stakeholders and analytics teams to facilitate self-service BI and reporting.
Data Desgine architucture(Data warehouse/datalake/datalakehouse/datamesh)
Approch to design(data medallian architecture)
### 2- BI: Analytics & Reporting (Data Analysis)
### 🎯 Objective
Develop SQL-based analytics to deliver detailed insights into:

Customer Behavior
Product Performance
Sales Trends

## 🏗️ Data Architecture
We have to specify which approach we want to follow, in our project we choose data modeluian architecture:

![image](https://github.com/user-attachments/assets/6a85e105-566d-4c2b-b208-b43b02a3fd72)

## What is Datawarehouse?
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
![image](https://github.com/user-attachments/assets/2cb2e5a3-48de-405e-8942-ea3b6da19309)


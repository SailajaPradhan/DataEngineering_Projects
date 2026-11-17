# 1_ADF_Databricks_Synapse  End-to-End Pipeline
This project implements the Medallion Architecture (Bronze, Silver, Gold) to ingest raw data from HTTP sources, transform it using distributed computing, serve analytical models, and create business ready data for visualization and reporting purposes.

### 🔄 Medallion Architecture Workflow

| Layer | Azure Service | Storage Format | Primary Tech | Core Objective |
| :--- | :--- | :--- | :--- | :--- |
| **🥉 Bronze** | Azure Data Factory + ADLS Gen2 | Raw (`JSON` / `CSV`) | Low-Code Pipelines | Exact copy of source data with ingestion metadata. |
| **🥈 Silver** | Azure Databricks + ADLS Gen2 | Delta / Parquet | **Python (PySpark)** & **SQL** | Data cleansing, deduplication, schema enforcement, and type casting. |
| **🥇 Gold** | Azure Synapse Analytics | Relational Views / Tables | **T-SQL** | Business-level aggregations, star-schema modeling, and BI serving. |

### 🛠️ Step-by-Step Pipeline Breakdown

#### 1. 🥉 Bronze Layer: Automated Ingestion (Azure Data Factory)
* **Source Connection:** Configured parameterized HTTP linked services and datasets in **Azure Data Factory (ADF)** to dynamically fetch data from external APIs.
* **Orchestration:** Built resilient pipelines with retry policies and dynamic folder partitioning (`YYYY/MM/DD`) to land raw data directly into the **ADLS Gen2 (Bronze container)**.
* **Outcome:** Immutable historical archive of raw source data.

#### 2. 🥈 Silver Layer: Distributed Transformation (Azure Databricks)
* **Integration:** Mounted ADLS Gen2 to **Azure Databricks** securely using Azure Key Vault and Service Principals.
* **Processing (Python & SQL):** 
  * Utilized **PySpark** to handle missing values, drop duplicates, standardize date formats, and enforce strict schemas.
  * Used **Spark SQL** to join normalized datasets and apply business rules.
* **Storage:** Wrote cleansed, ACID-compliant data back to **ADLS Gen2 (Silver container)** in **Parquet/Delta** format for optimized read performance.

#### 3. 🥇 Gold Layer: Data Warehousing & Serving (Azure Synapse)
* **Serverless SQL Pool:** Connected **Azure Synapse Analytics** directly to the Silver layer in ADLS Gen2.
* **Dimensional Modeling (SQL):** Created analytical **Views** and **CETAS (Create External Table As Select)** using T-SQL to structure data into a Star Schema (Fact and Dimension tables) optimized for fast querying.


### 4. 📊 Reporting & Analytics (Power BI)
* **BI Integration:** Connected **Power BI** directly to the Azure Synapse Gold Layer.
* **Visualization:** Built interactive executive dashboards featuring KPIs, trend analysis, and drill-down capabilities to drive data-informed decision-making.

### 🚀 Key Engineering Highlights
* **Scalability:** Decoupled storage (ADLS Gen2) and compute (Databricks & Synapse Serverless) to optimize cloud costs.
* **Dynamic Pipelines:** Parameterized ADF workflows allow seamless onboarding of new HTTP endpoints without code duplication.
* **Query Performance:** Partitioned Parquet storage combined with Synapse T-SQL views ensures sub-second dashboard rendering in Power BI.


-------------------------------------------------------------------------------------------------------------------------------------------
# 2_Databricks_medallion_processing (E-Commerce Data Engineering & Analytics Platform)
### Project Overview:
This portfolio project demonstrates an end-to-end data engineering and analytics architecture for an on-premises e-commerce store. Customer transactions are captured in an operational relational database, extracted using Python, stored in Amazon S3, and processed in Databricks using the Medallion Architecture.

The curated data is modeled into fact and dimension tables for analytical reporting. Databricks SQL dashboards provide business insights, while Databricks Genie enables users to explore business data using natural-language questions.


### Architecture:
#### End-to-End Data Flow

1.  **Customer Transactions:** Customers place orders through the e-commerce application.
2.  **OLTP Database:** The application server writes operational  transactions to the on-premises relational database.
3.  **Data Extraction:** Python connects to the relational database and pulls data for analytical processing.
4.  **Cloud Storage:** Extracted data is stored in Amazon S3, which acts as the landing and storage location for the Databricks pipeline.
5.  **Databricks Processing:** Databricks reads data from S3 and performs ETL/ELT, data quality checks, transformations, and analytical modeling.
6.  **Data Serving:** Curated Gold-layer data is made available to BI reports and dashboards for business users.


### Medallion Architecture
The Databricks pipeline organizes data into three layers: Bronze, Silver, and Gold. Each layer progressively improves data quality and usability.

#### 1. Bronze Layer -- Raw Data
-   Load extracted relational database data from Amazon S3.
-   Store raw data in Delta tables.
-   Retain source structure and values to support traceability and reprocessing.
-   Add ingestion metadata, such as load timestamp or source file, where applicable.
**Outcome:** A historical, raw representation of the source data.

#### 2. Silver Layer -- Cleaned and Transformed Data
-   Handle null values, duplicates, and invalid records.
-   Standardize data types, dates, currency values, and text fields.
-   Apply business rules and data validation checks.
-   Join and integrate related datasets where needed.
-   Prepare consistent customer, product, order, and transaction data for modeling.
**Outcome:** Cleansed, validated, and integrated Delta tables ready for analytical modeling.

#### 3. Gold Layer -- Business-Ready Data
The Gold layer uses a **star schema** with a central fact table connected to descriptive dimension tables.


### Technology Stack and Development:

| Technology | Purpose |
|---|---|
| On-premises relational database | Stores operational e-commerce transactions. |
| Python | Extracts data from the relational database and supports ingestion workflows. |
| Amazon S3 | Stores extracted source data for cloud-based processing. |
| Databricks | Provides the data engineering and analytics environment. |
| PySpark | Supports distributed data transformations and processing. |
| SQL | Performs data transformations, joins, aggregations, and analytical queries. |
| Delta Lake | Provides reliable table storage for the Medallion layers. |
| Databricks Genie | Allows users to ask natural-language questions about business data. |
| Databricks SQL Dashboards | Presents KPIs and business trends through visual reports. | 


### Key Learning Outcomes:

This project demonstrates practical experience with:
-   End-to-end data movement from an on-premises relational database to cloud storage and Databricks.
-   Python-based data extraction and ingestion.
-   AWS S3 as a data landing and storage layer.
-   Databricks ETL/ELT development using Python, PySpark, and SQL.
-   Medallion Architecture and Delta Lake.
-   Dimensional modeling using fact and dimension tables.
-   Star-schema design for business intelligence.
-   Natural-language data exploration with Databricks Genie.
-   KPI development and dashboard creation using Databricks SQL.

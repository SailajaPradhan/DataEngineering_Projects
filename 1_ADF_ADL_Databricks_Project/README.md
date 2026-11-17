# ADF_Databricks_Synapse  End-to-End Pipeline
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

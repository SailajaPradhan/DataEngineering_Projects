# E-Commerce Data Engineering & Analytics Platform

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

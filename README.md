# Database_Migration: Azure_ETL_Pipeline
## Aim:
The primary goal is to design and implement a scalable ETL pipeline that extracts data from an on-premise SQL Server database representing Adventure Works, transforms it into a suitable format for analysis, and loads it into Azure Synapse Analytics Warehouse for further processing and visualization.

## Azure Services Used:
1. Azure Strorage Account:
2. Azure Data Factory:
3. Azure Databricks:
4. Azure Synapse Analystics:
5. Azure Key Vault:

## Project Components:
<p align='center'>
  <img src="images/etl-process-image.png">
</p>

- **Data Extraction:**  
  Source Database (On-Premise SQL Server): Data is extracted from the existing AdventureWorks database hosted on an on-premise SQL Server. The data includes only the tables with *SalesLT* schema.  
- **Data Transformation:**  
   Performing data cleansing, and Implementing transformations to convert raw data into formats suitable for analytical processing using pyspark in Azure Databricks.  
- **Data Loading:**  
  Azure Data Lake Storage: Transformed data is loaded into Azure Data Lake Storage for secure and scalable storage.  
  Azure Synapse Data Lakehouse: Alternatively, the transformed data can be stored in Azure Synapse Data Lakehouse as *Views* to analyze and extract insights and generate reports, visualizations down the line.

## Project Architecture:
<p align='center'>
  <img src="images/Etl_Architecture.png">
</p>

**EXTRACTION:**
  • In the extraction phase we have Azure Data Factory (ADF) copying the data into an Azure
  Storage which could be an Azure Data Lake or Azure Blob Storage. Here we have Azure
  Datalake Gen2.
  • We land the data in storage because of the future possibilities of combining and enriching the
  data with unstructured/semi-structured data from other sources. Since the daily incremental
  changes would be maintained in the Azure Storage the data lends itself to historical analysis
  as well.
  • Even though Azure Databricks could hit the SQL Server database via JDBC directly, we’re
  not doing it because we want to leverage the power of Databricks for transformation and not
  extraction.

**TRANSFORMATION:**
  • In the transform phase we have Databricks loading the file from a mount point into a dataframe,
  performing transformations and finally writing to a delta store. The following are some of
  highlights of the work done.
  • With the combination of Azure Datalake and Azure Databricks, we can create a lakehouse
  architecture that follows three layer of data processing:
  1. Bronze Layer - This is the exact copy of the data source, in its raw form. All the tables
  (relational model) or any unstructured data (Non-relational model) is stored in this layer.
  No transformations are done.
  2. Silver Layer - In this step, soft data transformations are performed such as fixing data
  types, column names, date formats, etc. to a standardized format and store in a more
  structured way.
  3. Gold Layer - This layer is the cleanest form of data that can be used for downstream
  tasks. Number of other things could also be implemented at this stage like business rules,
  conformity checks, etc.

**LOAD & VISUALIZATION:**
  • In this phase Transformed data from gold layer gets loaded onto Azure Syanpse Analytics
  Data Warehouse available in corresponding work space to leverage the analytical performance.
  • PowerBI a powerful visualization tool is connected to data warehouse in Azure Synapse
  Analytics data warehouse which was created earlier to directly query the data and to create
  responsive as well as interactive reports.




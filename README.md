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

- **Data Extraction:** Source Database (On-Premise SQL Server): Data is extracted from the existing AdventureWorks database hosted on an on-premise SQL Server. The data includes only the tables with *SalesLT* schema.  
- **Data Transformation:**  Performing data cleansing, and Implementing transformations to convert raw data into formats suitable for analytical processing using pyspark in Azure Databricks.  
- **Data Loading:** Azure Data Lake Storage: Transformed data is loaded into Azure Data Lake Storage for secure and scalable storage.  
Azure Synapse Data Lakehouse: Alternatively, the transformed data can be stored in Azure
Synapse Data Lakehouse as *Views* to analyze and extract insights and generate reports, visualizations down the line.

## Project Architecture:




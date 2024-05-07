## Aim:
The primary goal is to design and implement a scalable ETL pipeline that extracts data from an on-premise SQL Server database representing Adventure Works, transforms it into a suitable format for analysis, and loads it into Azure Synapse Analytics Warehouse for further processing and visualization.

## Azure Services Used:
1. Azure Strorage Account:
2. Azure Data Factory:
3. Azure Databricks:
4. Azure Synapse Analystics:
5. Azure Key Vault:

## Project Components:
**Data Extraction:** Extracting data from the on-premise SQL Server database. The data includes only the tables with *SalesLT* schema.  
**Data Transformation:**  Performing data cleansing, and Implementing transformations to convert raw data into formats suitable for analytical processing.  
Applying business rules and logic to derive meaningful insights from the data.  
**Data Loading:** Loading transformed data into Azure Syanapse Warehouse as *Views* to analyze and extract insights and generate reports, visualizations down the line.  

# Azure Databricks
Azure Databricks provides both computation and infrastruture to run **spark** code which is an open source distributed computation ***in-memory*** framework. None the less, SQL and python scripts can also be executed.  
  
In order to execute an piece of code, a computaion resource aka **compute cluster** is required. It is created and configured manually based on the required usage. Configuration of a compute cluster is defined by **Node Type** which usually includes:
- Number of **Cores**
- **Memory** of compute

> NOTE: The fewer configurations, the cheaper the compute cost. 

Within this project, Databricks is utilized to execute transformation notebooks of Pyspark code that carry out the cleaning and purification of the data extracted from the SQL server and stored in ADLS.

## NOTEBOOKS

For any Databricks workspace to read/write data from an ADLS conatiner, the workspace has to be mounted to that particular container through a mount point. A mount point of databricks is used/refers to a directory instance which is used to access a corresponding container in ADLS.
- <a href="StorageAccMount.ipynb">MOUNT STORAGE ACCOUNT</a>

Given that Medallion Architecture is the project's model, there are two Transformation Notebooks.
- <a href="Level 1 Transformation.ipynb">BRONZE TO SILVER (LEVEL 1)</a>
- <a href="Level 2 Transformation.ipynb">SILVER TO GOLD (LEVEL 2)</a>

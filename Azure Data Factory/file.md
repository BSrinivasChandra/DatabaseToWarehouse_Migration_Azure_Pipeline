# AZURE DATA FACTORY

The main task of this pipeline is to extract all the tables with 'SalesLT' schema from Adventure Work database residing in an onpremise sql server and load into Bronze container of Azure Data Lake Gen2(ADLS) which then is transformed recursively according to Level-1 & Level-2 transformation and loaded them into corresponding silver & gold container in ADLS.  
  
The pipeline mainly consists of four activities:
1. Look-Up Activity: _Lookup_ Activity can be used to dynamically determine which “Objects” to operate instead of hardcoding the “Object” name. Some “Object” examples are - *_Files_* and *_Tables_*. It returns a dictonary with keys 'count' and 'value'.
2. For-Each Acticity: _ForEach_ activity is used to iterate over a collection and executes specified activities in a loop.
3. Copy Activity: 
4. Notebook Activity:
<p align='center'>
  <img height =  200, src='ADF_ETL_FinalPipleline.png'>
</p>

<p align = 'center'><b>FINAL ADF PIPELINE</b></p>

<p align='center'>
  <img height =  250, src='LinkedServices.png'>
</p>
    
1. **LOOKUP ACTIVITY:**

<p align='center'>
  <img height =  500, src='LookUp Activity/Lookup_Setiitngs.png'>
</p>
<p align='center'>
  <img height =  150, src='LookUp Activity/SQLQuery_SaleasLT_Tables.png'>
</p>

```sql 
SELECT s.name as SchemaName, t.name TableName FROM sys.tables as t
INNER JOIN sys.schemas as s
ON s.schemaid = t.schemaid
WHERE s.name = 'SalesLT';
```
<p align='center'>
  <img height =  300, src='LookUp Activity/LookUp_Activity_Dataset.png'>
</p>

2. **FOR-EACH ACTIVITY:**
<p align='center'>
  <img src='ForEach Activity/ForEach_Settings.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_Expression.png'>
</p>

- **COPY ACTIVITY:**
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Source.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Source_Expression.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Source_Dataset.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivty_Sink.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivty_Sink_Dataset.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Sink_FileExpression.png'>
</p>
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Sink_FolderExpression.png'>
</p>

3. **NOTEBOOK ACTIVITY(LEVEL1):**
<p align='center'>
  <img src='Notebook Activity/BronzeToSilver_Level1_TrasformationNotebook.png'>
</p>

4. **NOTEBOOK ACTIVITY(LEVEL2):**
<p align='center'>
  <img src='Notebook Activity/SilverToGold_Level2_Trasnformation_Notebook.png'>
</p>

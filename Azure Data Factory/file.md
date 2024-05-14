# AZURE DATA FACTORY

The main task of this pipeline is to extract all the tables with 'SalesLT' schema from Adventure Work database residing in an onpremise sql server and load into Bronze container of Azure Data Lake Gen2(ADLS) which then is transformed recursively according to Level-1 & Level-2 transformation and loaded them into corresponding silver & gold container in ADLS.  
  
The pipeline mainly consists of four types of activities:
1. **LookUp Activity** : _Lookup_ Activity can be used to dynamically determine which “Objects” to operate instead of hardcoding the “Object” name. Some “Object” examples are - *_Files_* and *_Tables_*. It returns a dictonary with keys 'count' and 'value'.

>NOTE : LookUp activity is mainly used when there are multiple files or tables to deal with in one go.

2. **ForEach Activity** : _ForEach_ activity is used to iterate over a collection and executes specified activities in a loop.
3. **Copy Activity** : As the name suggests _Copy_ activity is used to “Copy” the Data from the data sources, located in “On-Premise” or “Cloud”. Once, the data is copied, it can be used in other Activities to further Transform and Analyze.
4. **Notebook Activity** : The Notebook activity in ADF pipeline allows you to run Notebook created in Azure Databricks.

</br><p align='center'>
  <img height =  200, src='ADF_ETL_FinalPipleline.png'>
</p>

<p align = 'center'><i>Final Pipeline.</i></p>
</br>

<p align='center'>
  <img height =  250, src='LinkedServices.png'>
</p>
<p align = 'center'><i>Linked Services.</i></p></br>
    
## 1. LookUp Activity:
This acticivity retrives all the table names along with its schema name associated with 'SalesLT' schema from Adventure Words Db in sql server. A key-value pair dictionary is generated conatining 'count' & 'value' then, passed onto the further activity i.e.., ForEach.</br>

> *_count_* -> Total No.of Items </br>*_value_* -> List of dictionaries which consists SchemaName & TableName.

</br><p align='center'>
  <img height =  500, src='LookUp Activity/Lookup_Setiitngs.png'>
</p>
<p align='center'><i>LookUp Activity.</i></p></br>

>NOTE : SQL Query returns a result set containing SchemaName & TableName.</br>
```sql 
SELECT s.name as SchemaName, t.name TableName FROM sys.tables as t
INNER JOIN sys.schemas as s
ON s.schemaid = t.schemaid
WHERE s.name = 'SalesLT';
```
<p align = 'center'><i>SQL Query</i></p>

</br><p align='center'>
  <img height =  300, src='LookUp Activity/LookUp_Activity_Dataset.png'>
</p>
<p align='center'><i>LookUp Activity Source Dataset.</i></p></br>

## 2. ForEach Activity:
This activity is like a loop which iterates over the 'value' from the output of lookup activity. As any loop conatins a statement to execute likewise this acitvity containes sub-activities within itself which are perfomed on each item over the iteration.  </br>
As we wish to copy the tables, we use *Copy* activity in ForEach activity which copies each table in every iteration.
</br><p align='center'>
  <img src='ForEach Activity/ForEach_Settings.png'>
</p>
<p align = 'center'><i>ForEach Activity.</i></p>

As the output from *_LookUp_* acitvity contains *count* & *value*, we only need *value* to iterate over the names of tha table. So, an expression in written which returns only *value* from the output of *_LookUp_* activity.
<p align='center'>
  <img src='ForEach Activity/ForEach_Expression.png'>
</p>
<p align = 'center'><i>Expression of ForEach.</i></p>

### Copy Activity (ForEach):
This *Copy activity* copies each table for every time it iterates over the *ForEach* activity.
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Source.png'>
</p>
<P align='center'><i>Copy Activity Source</i></P>

To get *SchemaName* & *TableName* from *ForEach* activity for every iteration we use the following expression.
<p align='center'>
  <img src='ForEach Activity/ForEach_CopyActivity_Source_Expression.png'>
</p>
<p align='center'><i>Expression of Copy Activity (ForEach).</i></p>

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

## 3. NOTEBOOK ACTIVITY(LEVEL1)
<p align='center'>
  <img src='Notebook Activity/BronzeToSilver_Level1_TrasformationNotebook.png'>
</p>

## 4. NOTEBOOK ACTIVITY(LEVEL2):
<p align='center'>
  <img src='Notebook Activity/SilverToGold_Level2_Trasnformation_Notebook.png'>
</p>

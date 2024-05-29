# Azure Synapse Analytics

The task of this pipeline is to create ***views*** of the files which are transformed and stored in *gold* container so that they can be further analysed either through *SQL* or *PowerBI*.  

A database named ***gold_db*** is created prior to the execution of the pipeline which is where all the views will be stored.   

Further the creation of the views, *SQL* queries can be executed on them to *analyze* the data. Additionaly to that, views can be loaded or queried directly through *PowerBI* to generate *Interactive Reports*.

<p align = 'center'>
    <img src = 'Synapse FInal Pipeline.png'>
</p>
<p align = 'center'><i>Views Creation Pipeline</i></p>

## Get MetaData Activity
<p align = 'center'>
    <img src = 'Get MetaData Activity\GetMetaData_Activity.png'>
</p>
<p align = 'center'><i>Get MetaData Activity</i></p>

<p align = 'center'>
    <img src = 'Get MetaData Activity\GetMetaData_Activity_Dataset.png'>
</p>
<p align = 'center'><i>Get MetaData Dataset</i></p>

## ForEach Activity
<p align = 'center'>
    <img src = 'ForEach Activity\ForEach_Acivity.png'>
</p>
<p align = 'center'><i>ForEach Acivity</i></p>

<p align = 'center'>
    <img src = 'ForEach Activity\ForEach_Activity_Expression.png'>
</p>
<p align = 'center'><i>ForEach Activity Expression</i></p>

<p align = 'center'>
    <img src = 'ForEach Activity\ForEach_Acivity_StoredProcedure.png'>
</p>
<p align = 'center'><i>ForEach Acivity StoredProcedure</i></p>
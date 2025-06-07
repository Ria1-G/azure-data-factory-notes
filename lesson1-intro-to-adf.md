# 🎬 Lesson 1: Introduction to Azure Data Factory 

⏱️ Timestamp: 00:00 - 13:35

## 🔑 Key Concepts
- Azure Data Factory (ADF) is a cloud-based data integration service.
- Enables data movement, transformation, scheduling, and monitoring.
- Thus its a cloud based ETL/ELT tool.
- Has connectors for all the sources(SQLdb, csv files, api, http) and also for the destinations(Azure data lake, S3, Azure sql db ,   
  Dataverse,etc). Thus 'E' and 'L' is done.
- For 'T' -> Has Data Flows = viz the transformation functionalities which the ADF possess. Spark clusters run behind the Data flows.

## 🛠️ Components Introduced
- **Linked Service** – Connects to sources like Azure SQL, Blob, etc.You need to build a connection from source to ADF and from ADF to destination. This connection is called LS.
- **Dataset** – Data structures like tables, files, etc.In a SQL DB , we have multiple tables T1, T2 ,T3 ,etc and different views like V1 ,V2 ,V3 ,etc. Suppose i want to migrate T3 to ADF. That becomes my dataset. Thus its used to identify which data needs to be migrated.Dataset used in destination as well.
- **Pipeline** – Collection of activities like Copy, Lookup.

## Services Introduced
- **Resource Groups** - Whatever resource is created in azure requires a resource group.
- **Resource** - Its a service we use in azure (ADF, Synapse analytics, Storage acccount)
- **Azure Data Lake** - No data lake in azure. It rather has storage accounts. Insdide it , we have Blob storage. But if we dont want blob storage ,instead want data lake ,theres a configuration which we have to do.
**Blob storage vs Data Lake** - In blob storage we only get containers, but in data lake we can use heirarchy and namespaces (folders inside folders to store our data)


## 💬 Quotes/Concepts from Ansh:
> "ADF is there in Synapse analytics and fabric. ADF is always there."

## 📌 My Observations
- GUI makes it easy for non-coders to build pipelines.
- Great for enterprise-scale ETL workflows.

## 🧠 To Revisit
- Difference between Integration Runtime vs Linked Service


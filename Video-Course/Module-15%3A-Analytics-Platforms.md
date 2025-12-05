# Overview
---
At this point, more than 75% complete at 76% complete. I'm such a nerd.

# Module 15: Analytics Platforms
---

## Analytics Platforms
    - Azure Synapse Analytics
    - Azure Synapse Link
    - Azure Data Factory
    - Azure Databricks

# Azure Data Lake Storage
---
ADLS Gen2 - Azure Data Lake Storage Gen2 is a highly scalable and secure data lake solution built on top of Azure Blob Storage. It provides a hierarchical namespace, which allows for organizing data in a directory-like structure, making it easier to manage and analyze large volumes of data. ADLS Gen2 is designed for big data analytics workloads and supports features such as fine-grained access control, high throughput, and low latency. It is commonly used for storing and analyzing large datasets in scenarios such as data warehousing, machine learning, and real-time analytics.

Key Features:
- Hierarchical namespace: Organize data in a directory-like structure for easier management.
- Fine-grained access control: Implement security at the file and folder level.
- High throughput: Optimize performance for big data analytics workloads.
- Low latency: Ensure fast access to data for real-time analytics.
- Hadoop HDFS compatibility: Integrate with Hadoop ecosystem tools for big data processing.
- Massive scale
- built on blobs
- POSIX compliant access control lists (ACLs)
- Cost efficient storage for big data analytics workloads

Watch out for egress charges when moving data out of Azure Data Lake Storage Gen2 to other regions or services. Consider using Azure Data Factory or Azure Synapse Link for data movement and integration to minimize costs.

# Azure Synapse
---
Enterprise data warehousing and big data analytics solution that combines data integration, data warehousing, and big data analytics into a single service. It provides a unified experience for ingesting, preparing, managing, and serving data for immediate business intelligence and machine learning needs.

Key Features:
- Data integration: Seamlessly integrate data from various sources using Azure Data Factory.
- Data warehousing: Create and manage data warehouses with SQL-based analytics.
- Big data analytics: Analyze large volumes of data using Apache Spark and SQL.
- Serverless on-demand querying: Run queries on data stored in Azure Data Lake Storage Gen2 without the need to provision infrastructure.
- Built-in security and compliance: Ensure data protection with features like encryption, access control, and auditing.
- Integration with Azure Machine Learning: Enable advanced analytics and machine learning capabilities directly within the Synapse environment.
- Real-time analytics: Use Azure Stream Analytics to process streaming data in real-time for immediate insights.

Data Scientists and Data Engineers can use Azure Synapse to build and deploy machine learning models, perform data transformations, and create data pipelines for data processing and analysis.

Architecture:
- Azure Data Lake Storage
- Synapse workspace
- Analytics pools (SQL, Spark)
- Networking and security components (Virtual Network, Private Link, Firewall rules)

## Analytics Pools
---
- SQL Dedicated Pools: Dedicated SQL pools for data warehousing and analytics workloads.
- Spark Pools: Apache Spark pools for big data analytics and machine learning workloads.
- Serverless SQL Pools: On-demand querying of data stored in Azure Data Lake Storage Gen2 without the need to provision infrastructure.
- Spark Dedicated Pools: Dedicated Spark pools for big data analytics and machine learning workloads.
Note: SQL Dedicated Pools you get read, Spark Dedicated Pools, read/write. Serverless SQL Pools, read only.
SQL Dedicated pools, T-SQL, Spark Dedicated Pools, Spark SQL. Serverless SQL Pools, T-SQL.

# Databricks
---
Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud services platform. It provides a collaborative environment for data scientists, data engineers, and business analysts to work together on big data analytics and machine learning projects. Azure Databricks offers a fully managed service that simplifies the deployment and management of Apache Spark clusters, allowing users to focus on their data and analytics tasks rather than infrastructure management.

Compared to Synapse, Azure Databricks is more focused on data engineering and machine learning workloads, while Synapse is more focused on data warehousing and big data analytics. Azure Databricks provides a collaborative workspace for data scientists and engineers to work together on data projects, while Synapse provides a unified experience for data integration, warehousing, and analytics.

Databricks is also called a Lakehouse, which is a combination of a data lake and a data warehouse. It allows you to store raw data in a data lake and then use SQL or Spark to query and analyze that data, providing the benefits of both a data lake and a data warehouse.

Implementation:
- Create a Databricks workspace in Azure inside of a resource group
- Create a Databricks cluster with the appropriate configuration for your workload (e.g., number of nodes, instance types, etc.)
- Use the Databricks workspace to create notebooks for data analysis and machine learning tasks
- Use the Databricks workspace to create jobs for scheduling and automating data processing tasks

# Azure Data Factory
---
Azure Data Factory is a cloud-based data integration service that allows you to create, schedule, and orchestrate data pipelines to move and transform data from various sources to various destinations. It provides a visual interface for designing data workflows and supports a wide range of data sources and destinations, including on-premises and cloud-based data stores. Azure Data Factory enables you to create data-driven workflows for orchestrating and automating data movement and data transformation. It also provides features for monitoring and managing data pipelines, making it easier to ensure data quality and reliability. Azure Data Factory is commonly used for scenarios such as data migration, data integration, and data transformation in the cloud.

Architecture:
- Data Factory: The main service that orchestrates data movement and transformation.
- Pipelines: A logical grouping of activities that perform a specific task.
- Activities: The individual tasks that perform data movement or transformation.
- Triggers: Schedules or events that initiate pipeline execution.
- Use Azure Data Factory to create pipelines that move data from on-premises sources to Azure Data Lake Storage Gen2, and then use Azure Synapse or Azure Databricks to analyze the data
- Azure, Self-hosted and SSIS Integration Runtime: The compute infrastructure used to execute data movement and transformation activities. Azure Integration Runtime is used for cloud-based data movement, while Self-hosted Integration Runtime is used for on-premises data movement. SSIS Integration Runtime is used for executing SQL Server Integration Services (SSIS) packages in the cloud.

Demo: Configure Data transformation with Azure Data Factory (ADF)
---
1. Create a new Azure Data Factory instance in the Azure portal.
2. Create a new pipeline in the Data Factory.
3. Add a new activity to the pipeline, such as a Copy Data activity.
4. Configure the source and destination for the Copy Data activity, such as an on-premises SQL Server database and an Azure Data Lake Storage Gen2 account.
5. Set up the necessary linked services and datasets for the source and destination.
6. Configure any necessary transformations or mappings for the data movement, such as data type conversions or column mappings.
7. Test the pipeline to ensure that the data is being moved correctly from the source to the destination.
8. Schedule the pipeline to run at specific intervals or trigger it based on events, such as the arrival of new data in the source system.

Note: You use the Azure Data Factory Studio to create and manage your data pipelines. The Studio provides a visual interface for designing and orchestrating your data workflows, allowing you to easily create and manage your data integration processes. You can use the Studio to create pipelines, add activities, configure linked services and datasets, and monitor the execution of your pipelines.

# Case Study: Design Analytics Platform
---
On premises data
not publicly accessible
Reporting Team
Need to build Power BI reports once every 2 weeks
Ensure Cosmos DB data is real time

Question:
How would you configure Storage for Synapse
what analytics pools would you recommend

Solution:
We have on prem data in JSON, we have Cosmos DB data in Azure in JSON.
We need Azure Synapse and an Azure Data Lake Storage account
Connect Synapse link for the Cosmos DB data to the Data Lake Storage account
Use Azure Data Factory to move the on prem data to the Data Lake Storage account
Use Azure Synapse to create a SQL Dedicated Pool for the data warehousing and analytics workloads.
Build a serverless SQL pool for querying the data in the Data Lake Storage account without needing to provision infrastructure.



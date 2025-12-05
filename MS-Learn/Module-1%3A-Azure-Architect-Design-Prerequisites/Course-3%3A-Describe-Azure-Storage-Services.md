# Link
---
https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/

46 minutes

# Introduction
---
* Compare Azure storage services.
* Describe storage tiers.
* Describe redundancy options.
* Describe storage account options and storage types.
* Identify options for moving files, including AzCopy, Azure Storage Explorer, and Azure File Sync.
* Describe migration options, including Azure Migrate and Azure Data Box.

# Describe Azure Storage Accounts
---
Azure Storage Accounts provide a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS. They are used to store and manage data in Azure, including blobs, files, queues, tables, and disks. Azure Storage Accounts offer different types of storage services, each designed for specific use cases and performance requirements.

Note: Memorize these...
Probably the most important thing to remember here are the different types of redundancy options, which include:
- Locally-redundant storage (LRS): Replicates data three times within a single data center in the same region.
- Geographically-redundant storage (GRS): Replicates data to a secondary region hundreds of miles away from the primary region for disaster recovery.
- Read-access geo-redundant storage (RA-GRS): Similar to GRS, but also allows read access to the secondary region in case the primary region is unavailable.
- Zone-redundant storage (ZRS): Replicates data across three availability zones within the same region for high availability and durability.
- Geo-zone-redundant storage (GZRS): Combines the features of GRS and ZRS by replicating data across three availability zones in the primary region and replicating it to a secondary region for disaster recovery.
- Read access geo-zone-redundant storage (RA-GZRS): Similar to GZRS, but also allows read access to the secondary region in case the primary region is unavailable.

Oh, and memorize these too:
-Standard General-purpose v2 storage accounts: These are the most common type of storage accounts and support all Azure Storage services, including blobs, files, queues, tables, and disks. They offer a wide range of features and performance options.
- Premium Block Blobs: These storage accounts are optimized for high-performance workloads that require low latency and high throughput. They are designed for scenarios such as big data analytics, media processing, and high-performance computing.
- Premium File Shares: These storage accounts are optimized for high-performance file shares that require low latency and high throughput. They are designed for scenarios such as enterprise file shares, databases, and high-performance computing.
- Premium Page Blobs: These storage accounts are optimized for high-performance workloads that require low latency and high throughput. They are designed for scenarios such as virtual machine disks, databases, and high-performance computing.


Redundancy Options:
Standard General Purpose v2 Storage Accounts: LRS, ZRS, GRS, RA-GRS, GZRS, RA-GZRS
Premium Block Blob Storage Accounts: LRS, ZRS
Premium File Share Storage Accounts: LRS, ZRS
Premium Page Blob Storage Accounts: LRS

Benefits of Azure Storage Account Endpoints:
- Unique Namespace: Each storage account provides a unique namespace for your data, ensuring that your data is isolated and secure.
- All storage account names must be unique across Azure.
- 3-24 characters, numbers and lowercase letters only.

- Blob: blob.core.windows.net
- File: file.core.windows.net
- Queue: queue.core.windows.net
- Table: table.core.windows.net
- Data Lake Storage Gen2: dfs.core.windows.net

## Redundancy
---
You pretty much get what you pay for here. The more redundancy you want, the more it costs. Low cost------HA

Think about how your data is replicated in the primary region.
Then, think about whether your data is replicated to a secondary region that is geographically distant from the primary region.
Then finally, think about whether you need read access to the secondary region if the primary becomes unavailable. 

Data in a storage account is replicated three times in the primary region. You get two options for primary region replication:
- Locally-redundant storage (LRS)-11 9's of durability
- Zone-redundant storage (ZRS)-12 9's of durability

Local Redundant Storage (LRS):
If a disaster occurs in that data center, all three copies in LRS is at risk.
Same datacenter, 3 copies

Zone Redundant Storage (ZRS):
Data is replicated across three availability zones within the same region.
If a disaster occurs in one zone, the other two zones still have copies of the data.
Different datacenters, same region, 3 copies

Geo-Redundant Storage (GRS) and Read-Access Geo-Redundant Storage (RA-GRS):
- 16 9's of durability
Data is replicated to a secondary region that is hundreds of miles away from the primary region.
If a disaster occurs in the primary region, data can be recovered from the secondary region.
GRS: LRS in two different regions. No read access to secondary region
RA-GRS: LRS in two different regions. Read access to secondary region

Geo-Zone-Redundant Storage (GZRS) and Read-Access Geo-Zone-Redundant Storage (RA-GZRS):
- 16 9's of durability
Combines the features of GRS and ZRS by replicating data across three availability zones in the primary region and replicating it to a secondary region for disaster recovery.
GZRS: ZRS in primary region and LRS in secondary region. No read access to secondary region
RA-GZRS: ZRS in primary region and LRS in secondary region. Read access to secondary region

Note: GRS and GZRS can have read access in the secondary region IF Microsoft initiates a failover due to a disaster in the primary region. This is different from RA-GRS and RA-GZRS, which allow read access to the secondary region at any time, even if the primary region is still available.

# Describe Azure Storage Services
---
- Blobs: Binary Large Objects used for storing unstructured data such as images, videos, and documents.
- Files: Managed file shares that can be accessed via the SMB protocol.
- Queues: Messaging Stores for storing large numbers of messages that can be accessed from anywhere in the world.
- Tables: NoSQL key-value store for storing structured data.
- Disks: Block level storage used for virtual machines.
- Data Lake Storage (maybe): Blobs optimized for big data analytics workloads.

Benefits of Azure Storage Services:
- Scalability: Azure Storage Services can scale up or down based on your needs, allowing you to handle large amounts of data without worrying about capacity planning.
- Durability: Azure Storage Services are designed to provide high durability and availability, ensuring that your data is always accessible when you need it.
- Secure: Azure Storage Services provide built-in security features such as encryption, access control, and network security to help protect your data from unauthorized access.
- Managed: Azure Storage Services are fully managed by Microsoft, which means that you don't have to worry about maintenance, updates, or backups.
- Cost-effective: Azure Storage Services offer a pay-as-you-go pricing model, which means that you only pay for what you use, making it a cost-effective solution for storing and managing your data.
- Accessible: Azure Storage Services can be accessed from anywhere in the world over HTTP or HTTPS, making it easy to share and collaborate on data with others.
## Blob Storage
---
Blob storage is designed for storing large amounts of unstructured data, such as text or binary data. It is optimized for storing and retrieving large files, such as images, videos, and documents. I probably copied this from above so lets repeat it so you understand it.
- Accessible via HTTP/HTTPS anywhere in the world
- Types of blobs: block blobs, append blobs, page blobs
- Storage Tiers for different access types.

Storage Tiers:
- Hot Tier: Optimized for storing data that is accessed frequently. Higher storage costs, lower access costs.
- Cool Tier: Optimized for storing data that is accessed infrequently. Lower storage costs, higher access costs.
- Cold Tier: Optimized for storing data that is rarely accessed and has a minimum retention period of 90 days. Lower storage costs, higher access costs.
- Archive Tier: Optimized for storing data that is rarely accessed and can tolerate several hours of retrieval latency. Lowest storage costs, highest access costs.

Considerations:
- Hot Cool and cold can be set at the account level. Archive is a tier you can move data to.
- All tiers can be set at the blob level.
- Data in cool and cold tiers can tolerate lower availability but need high durability. Acceptable tradeoffs for cost savings.
- Archive storage stores data offline. Data must be rehydrated before it can be accessed, which can take several hours.

## Azure Files
---
Azure Files is a managed file share service that allows you to create file shares in the cloud that can be accessed via the SMB protocol. It is designed for scenarios where you need to share files between multiple virtual machines or applications.
- Accessible via SMB protocol or NFS protocols
- Can be mounted on Windows (SMB), Linux, and macOS (NFS)
- Supports Azure File Sync for caching and syncing files between on-premises and cloud

Benefits of Azure Files:
- Fully managed file shares in the cloud - you can replace your SMB or NFS file servers with this
- Accessible from anywhere via SMB or NFS
- Fully Managed: Microsoft handles maintenance, updates, and backups
- Integration with on-premises: Azure File Sync allows you to cache and sync files between on-premises and cloud
- Resilient: Built-in redundancy options to ensure high availability and durability
- Familiar: Access via file system I/O APIs and protocols. You can also use Azure Storage Client Libraries and Azure Storage REST APIs.

## Azure Queues
---
Used to store and manage messages that can be accessed from anywhere in the world over HTTP or HTTPS. It is designed for scenarios where you need to decouple application components and enable asynchronous communication between them.
Integrated with Azure Functions and Azure Logic Apps for serverless processing of messages.
- Accessible via HTTP/HTTPS anywhere in the world
- Used for decoupling application components and enabling asynchronous communication between them
- Messages can be up to 64 KB in size and can be retained for up to 7 days

## Azure Disks
---
Azure Disks are block-level storage volumes that can be attached to Azure Virtual Machines (VMs) to provide persistent storage. They are designed for scenarios where you need high-performance storage for applications running on VMs, such as databases, analytics workloads, and virtual desktops.
- Conceptually similar to on-premises disks, but in the cloud and virtualized.
- Can be used as OS disks, data disks, or temporary disks for VMs.
- Available in Standard and Premium performance tiers, with different levels of performance and durability.
- Standard Disks: Backed by HDDs, suitable for development and testing workloads, or workloads that do not require high performance. Lower cost, lower performance.
- Premium Disks: Backed by SSDs, suitable for production workloads that require high performance and low latency. Higher cost, higher performance.
- Ultra Disks: Backed by NVMe SSDs, suitable for data-intensive workloads that require the highest performance and lowest latency. Highest cost, highest performance.

## Azure Tables
---
Azure Tables is a NoSQL key-value store that allows you to store and manage structured data in the cloud. It is designed for scenarios where you need to store large amounts of structured data that can be accessed from anywhere in the world over HTTP or HTTPS. It is optimized for storing and querying large datasets with a flexible schema, making it ideal for scenarios such as IoT data, user data, and metadata storage.
- Accessible via HTTP/HTTPS anywhere in the world
- NoSQL key-value store for storing structured data
- Schema-less design allows for flexible data models
- Supports OData protocol for querying data
- Provides high availability and durability with built-in redundancy options

# Exercise: Create a storage blob
---
1. Log into the Azure portal and navigate to the Storage Accounts service.
2. Click on "Create" to create a new storage account.
3. Fill in the required fields, such as subscription, resource group, storage account name, region, and performance tier.
4. Choose the appropriate redundancy option based on your requirements.
5. Ensure that the Allow Enabling anonymous access on individual containers is checked (just for this exercise).
6. Click "Review + create" and then "Create" to create the storage account.

## Create a Container
---
1. Once the storage account is created, navigate to the storage account overview page.
2. Click on "Containers" under the "Blob service" section.
3. Click on "Create container" to create a new container.
4. Fill in the required fields, such as container name and public access level.
5. Click "Create" to create the container.

## Upload a Blob
---
1. Navigate to the container you just created.
2. Click on "Upload" to upload a new blob.
3. Select a file from your local machine to upload as a blob.
4. Click "Upload" to upload the file to the container.
Note: You may need to set the access level of the container to "Blob (anonymous read access for blobs only)" to allow public access to the blob so you can download and view it without authentication.

## Cleanup:
---
Delete the blob, container, and storage account to avoid unnecessary costs. You can do this by navigating to the storage account overview page, selecting the container, and then deleting the blob and container. Finally, delete the storage account itself.

Or, just delete the Resource Group that contains the storage account, which will delete all resources within it. :)

# Identify Migration options
---
Azure provides several options for migrating data to Azure Storage, including:
- Azure Migrate: A service that helps you discover, assess, and migrate on-premises servers, applications, and data to Azure.
- Azure Data Box: A physical device that you can use to transfer large amounts of data to Azure when network transfer is not feasible or would take too long.
- AzCopy: A command-line tool that allows you to copy data to and from Azure Storage accounts. It is designed for high-performance data transfer and can be used for both small and large data sets.

Azure Migrate is ideal for migrating on-premises servers, applications, and data to Azure. It provides a comprehensive assessment of your on-premises environment and helps you plan and execute your migration to Azure.
- unified migration experience for servers, applications, and data
- Discovery and assessment of on-premises environment
- Migration planning and execution tools

Integrated tools:
- Azure Migrate: Discovery and Assessment: Provides insights into your on-premises environment, including server inventory, performance metrics, and dependencies. It helps you identify migration candidates and plan your migration strategy.
- Azure Migrate: Server Migration: Provides tools for migrating on-premises servers to Azure, including support for both agent-based and agentless migration methods. It helps you migrate your servers with minimal downtime and provides options for testing and validating your migration before cutover.
- Azure Database Migration Service: Provides tools for migrating databases to Azure, including support for a wide range of database types and migration scenarios. It helps you migrate your databases with minimal downtime and provides options for testing and validating your migration before cutover.
- Azure App Service Migration Assistant: Provides tools for migrating web applications to Azure App Service, including support for a wide range of application types and migration scenarios. It helps you migrate your applications with minimal downtime and provides options for testing and validating your migration before cutover.
- Azure Data Box: A physical device that you can use to transfer large amounts of data to Azure when network transfer is not feasible or would take too long.

## Azure Data Box
--- It is ideal for scenarios where you need to transfer large amounts of data, such as when migrating large databases or file shares to Azure Storage. You can order a Data Box from the Azure portal, copy your data to the device, and then ship it back to Microsoft for upload to Azure Storage. This can be a cost-effective and efficient way to transfer large amounts of data to Azure, especially when network bandwidth is limited or when you need to transfer data quickly. 
The Data Box supports up to 80 TB of data and can be used for a variety of data transfer scenarios, including migrating large databases, file shares, and other types of data to Azure Storage. It is a secure and reliable way to transfer data to Azure, with built-in encryption and tamper-proof hardware to ensure the integrity and confidentiality of your data during transit.

Use Cases:
- Migrating large databases to Azure Storage
- moving media files to Azure Storage
- Transferring large file shares to Azure Storage
- historical data
- initial bulk data transfer for ongoing data migration projects
- Periodic uploads of large data sets to Azure Storage for backup or archival purposes

Export Use Cases:
- Disaster recovery scenarios where you need to quickly export data from Azure Storage to on-premises or other cloud environments
- Security Requirements - Government or security requirements that mandate physical transfer of data rather than over the network
- Migrate back to on-premises or other cloud environments when network transfer is not feasible or would take too long.

# Identify Azure File Movement Options
---
AzCopy: A command-line tool that allows you to copy data to and from Azure Storage accounts. It is designed for high-performance data transfer and can be used for both small and large data sets.
- One directional.

Azure Storage Explorer: A graphical user interface tool that allows you to manage and transfer data to and from Azure Storage accounts. It provides a user-friendly interface for browsing and managing your storage accounts, containers, and blobs, as well as for uploading and downloading files.
- Uses AzCopy under the hood for data transfer, but provides a more user-friendly interface for managing and transferring data to and from Azure Storage accounts.
Azure File Sync: A service that allows you to synchronize files between on-premises file servers and Azure Files. It provides a way to keep your on-premises file shares in sync with Azure Files, allowing you to take advantage of the scalability and durability of Azure Storage while still maintaining access to your files on-premises.
- Two directional sync between on-premises file shares and Azure Files, allowing you to keep your files in sync across both environments. It is designed for scenarios where you need to maintain access to your files on-premises while also taking advantage of the scalability and durability of Azure Storage.
- SMB, NFS, FTPS
- Have as many caches as you need.
- replace a failed local server by installing Azure File Sync on a new server and syncing the data from Azure Files to the new server.
- Configure cloud tiering so that the most frequently accessed files are stored locally on the server, while less frequently accessed files are stored in Azure Files. This can help optimize performance and reduce storage costs by keeping only the most important files on-premises while still providing access to all files in Azure Storage.
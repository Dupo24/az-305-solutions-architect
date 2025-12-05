# Appendix
##-
[[_TOC_]]

## Services Covered

## Compute
	- Azure Virtual Machines (VM)
	- Virtual Machine Scale Sets (VMSS)
	- Azure Kubernetes Service (AKS)
	- Azure Container Instances (ACI)
	- Azure App Service
	- Azure Functions
	- Azure Batch

## Storage
	- Azure Storage Accounts (Blob, Queue, Table)
	- Azure Blob Storage
	- Azure Files / Azure File Sync
	- Azure Managed Disks
	- Azure NetApp Files
	- Azure Data Lake Storage Gen2

## Databases & Analytics
	- Azure SQL Database
	- Azure SQL Managed Instance
	- Azure Synapse Analytics
	- Azure Synapse Link
	- Azure Cosmos DB
	- Azure Database for MySQL
	- Azure Database for PostgreSQL
	- Azure Database for MariaDB
	- Azure Cache for Redis

## Integration & Messaging
	- Azure Service Bus
	- Azure Event Grid
	- Azure Event Hubs
	- Azure Logic Apps
	- Azure API Management
	- Azure Data Factory

## Networking & Delivery
	- Azure Virtual Network (VNet)
	- Network Security Groups (NSG)
	- Azure Load Balancer
	- Azure Application Gateway (incl. WAF)
	- Azure Front Door
	- Azure Traffic Manager
	- Azure Content Delivery Network (CDN)
	- Azure VPN Gateway
	- Azure ExpressRoute
	- Azure Virtual WAN
	- Azure Route Server
	- Azure Bastion
	- Azure DDoS Protection
	- Azure Firewall
	- Azure Private Link / Service Endpoints

## Identity, Access & Security
	- Azure Active Directory (Azure AD)
	- Azure AD Domain Services (AAD DS)
	- Conditional Access / PIM
	- Azure Role-Based Access Control (RBAC)
	- Azure Key Vault
	- Microsoft Defender for Cloud (Security Center)
	- Microsoft Sentinel
	- Azure Policy / Blueprints

## Observability & Monitoring
	- Azure Monitor
	- Log Analytics
	- Application Insights
	- Network Watcher

## Backup, Recovery & Resilience
	- Azure Backup
	- Azure Site Recovery

## Management, Governance & DevOps
	- Azure Resource Manager (ARM)
	- Azure Automation
	- Azure Advisor
	- Azure Cost Management
	- Azure DevOps / GitHub (CI/CD)
	- Azure Blueprints
	- Azure Lighthouse

## Containers & Registry
	- Azure Container Registry (ACR)

## Other platform services
	- Azure App Configuration
	- Azure SignalR Service
	- Azure Managed Identities
	- Azure Policy Insights


# Skill Breakdown
---
- Design identity, governance, and monitoring solutions (25–30%)
- Design data storage solutions (20–25%)
- Design business continuity solutions (15–20%)
- Design infrastructure solutions (30–35%)

# Design Areas
---
## Design identity, governance, and monitoring solutions (25–30%)
- Design solutions for logging and monitoring
- Recommend a logging solution
- Recommend a solution for routing logs
- Recommend a monitoring solution
### Design authentication and authorization solutions
	- Recommend an authentication solution
	- Recommend an identity management solution
	- Recommend a solution for authorizing access to Azure resources
	- Recommend a solution for authorizing access to on-premises resources
	- Recommend a solution to manage secrets, certificates, and keys
### Design governance
	- Recommend a structure for management groups, subscriptions, and resource groups, and a strategy for resource tagging
	- Recommend a solution for managing compliance
	- Recommend a solution for identity governance

## Design data storage solutions (20–25%)
### Design data storage solutions for relational data
- Recommend a solution for storing relational data
- Recommend a database service tier and compute tier
- Recommend a solution for database scalability
- Recommend a solution for data protection

### Design data storage solutions for semi-structured and unstructured data
- Recommend a solution for storing semi-structured data
- Recommend a solution for storing unstructured data
- Recommend a data storage solution to balance features, performance, and costs
- Recommend a data solution for protection and durability

### Design data integration
- Recommend a solution for data integration
- Recommend a solution for data analysis

## Design business continuity solutions (15–20%)
### Design solutions for backup and disaster recovery
- Recommend a recovery solution for Azure and hybrid workloads that meets recovery objectives
- Recommend a backup and recovery solution for compute
- Recommend a backup and recovery solution for databases
- Recommend a backup and recovery solution for unstructured data

### Design for high availability
- Recommend a high availability solution for compute
- Recommend a high availability solution for relational data
- Recommend a high availability solution for semi-structured and unstructured data

## Design infrastructure solutions (30–35%)
### Design compute solutions
- Specify components of a compute solution based on workload requirements
- Recommend a virtual machine-based solution
- Recommend a container-based solution
- Recommend a serverless-based solution
- Recommend a compute solution for batch processing

### Design an application architecture
- Recommend a messaging architecture
- Recommend an event-driven architecture
- Recommend a solution for API integration
- Recommend a caching solution for applications
- Recommend an application configuration management solution
- Recommend an automated deployment solution for applications

### Design migrations
- Evaluate a migration solution that leverages the Microsoft Cloud Adoption Framework for Azure
- Evaluate on-premises servers, data, and applications for migration
- Recommend a solution for migrating workloads to IaaS and PaaS
- Recommend a solution for migrating databases
- Recommend a solution for migrating unstructured data

### Design network solutions
- Recommend a connectivity solution that connects Azure resources to the internet
- Recommend a connectivity solution that connects Azure resources to on-premises networks
- Recommend a solution to optimize network performance
- Recommend a solution to optimize network security
- Recommend a load-balancing and routing solution

# Documentation

Azure SQL: https://learn.microsoft.com/en-us/azure/azure-sql/?view=azuresql



# Services
---
## Compute
	- Azure Virtual Machines (VM)
	- Virtual Machine Scale Sets (VMSS)
	- Azure Kubernetes Service (AKS)
	- Azure Container Instances (ACI)
	- Azure App Service
	- Azure Functions
	- Azure Batch

## Storage
	- Azure Storage Accounts (Blob, Queue, Table)
	- Azure Blob Storage
	- Azure Files / Azure File Sync
	- Azure Managed Disks
	- Azure NetApp Files
	- Azure Data Lake Storage Gen2

## Databases & Analytics
### Azure SQL Database
###	Azure SQL Managed Instance
###	Azure Synapse Analytics
###	Azure Synapse Link
###	Azure Cosmos DB
###	Azure Database for MySQL
###	Azure Database for PostgreSQL
###	Azure Database for MariaDB
###	Azure Cache for Redis
###	Azure Databricks
###	Azure Data Factory
---
Used for integrating data from one place to another.
- Collect/Ingest data from various sources
- Store
- Transform
- Publish
- Monitor data pipelines and data flows

ETL - Extract, Transform, Load

## Integration & Messaging
	- Azure Service Bus
	- Azure Event Grid
	- Azure Event Hubs
	- Azure Logic Apps
	- Azure API Management
	- Azure Data Factory

## Networking & Delivery
	- Azure Virtual Network (VNet)
	- Network Security Groups (NSG)
	- Azure Load Balancer
	- Azure Application Gateway (incl. WAF)
	- Azure Front Door
	- Azure Traffic Manager
	- Azure Content Delivery Network (CDN)
	- Azure VPN Gateway
	- Azure ExpressRoute
	- Azure Virtual WAN
	- Azure Route Server
	- Azure Bastion
	- Azure DDoS Protection
	- Azure Firewall
	- Azure Private Link / Service Endpoints

## Identity, Access & Security
	- Azure Active Directory (Azure AD)
	- Azure AD Domain Services (AAD DS)
	- Conditional Access / PIM
	- Azure Role-Based Access Control (RBAC)
	- Azure Key Vault
	- Microsoft Defender for Cloud (Security Center)
	- Microsoft Sentinel
	- Azure Policy / Blueprints

## Observability & Monitoring
	- Azure Monitor
	- Log Analytics
	- Application Insights
	- Network Watcher

## Backup, Recovery & Resilience
	- Azure Backup
	- Azure Site Recovery

## Management, Governance & DevOps
	- Azure Resource Manager (ARM)
	- Azure Automation
	- Azure Advisor
	- Azure Cost Management
	- Azure DevOps / GitHub (CI/CD)
	- Azure Blueprints
	- Azure Lighthouse

## Containers & Registry
	- Azure Container Registry (ACR)

## Other platform services
	- Azure App Configuration
	- Azure SignalR Service
	- Azure Managed Identities
	- Azure Policy Insights

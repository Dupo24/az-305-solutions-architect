# Link
---
https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/

68 minutes

# Introduction
---
* Compare compute types, including container instances, virtual machines, and functions.
* Describe virtual machine options, including virtual machines (VMs), virtual machine scale sets, virtual machine availability sets, and Azure Virtual Desktop.
* Describe resources required for virtual machines.
* Describe application hosting options, including Azure Web Apps, containers, and virtual machines.
* Describe virtual networking, including the purpose of Azure Virtual Networks, Azure virtual subnets, peering, Azure DNS, VPN Gateway, and ExpressRoute.
* Define public and private endpoints.
# Describe Azure Virtual Machines
---
VMs are the most common compute resource in Azure. They provide on-demand, scalable computing resources that can be used to run applications, host websites, and perform various other tasks. Azure VMs can be created from a variety of images, including Windows and Linux operating systems, and can be customized with different sizes and configurations to meet specific workload requirements. Azure VMs can be used for a wide range of scenarios, including development and testing, running applications, hosting websites, and performing data analysis. They can also be used in combination with other Azure services, such as Azure Virtual Networks and Azure Storage, to create more complex solutions.

- Total control over the OS and applications
- Can run any workload that can run on a physical server
- custom hosting configurations
Image is a template used to create a VM. It contains the OS and any pre-installed software. You can use a marketplace image, a custom image, or a shared image from another subscription.

## Scale VMs in Azure
---
Azure Virtual Machine Scale Sets (VMSS) allow you to create and manage a group of identical, load-balanced VMs. VMSS can automatically scale the number of VMs in response to demand, making it easier to handle variable workloads. You can configure VMSS to scale based on metrics such as CPU usage, memory usage, or custom metrics. VMSS also provides high availability and fault tolerance by distributing VMs across multiple fault domains and update domains. This means that if one VM goes down, the others can continue to run without interruption. VMSS is ideal for scenarios such as web applications, big data processing, and container orchestration, where you need to handle variable workloads and ensure high availability.

- Scale based on demand or schedule
## Virtual Machine Availability Sets
---
Azure Virtual Machine Availability Sets are a way to ensure high availability for your VMs by grouping them together in a way that protects against hardware failures and maintenance events. When you create an availability set, Azure automatically distributes the VMs across multiple fault domains and update domains. This means that if one VM goes down due to a hardware failure or maintenance event, the other VMs in the availability set can continue to run without interruption. Availability sets are ideal for scenarios where you need to ensure high availability for your applications, such as web applications, databases, and other critical workloads.

Grouped in two ways:
- Update domains: VMs are grouped into update domains to ensure that not all VMs are updated at the same time during maintenance. This helps to maintain availability during updates.
- Fault domains: VMs are grouped into fault domains to ensure that they are distributed across different physical hardware to minimize the impact of hardware failures. This helps to improve the availability of the application.

No cost for availability sets. You pay for the VMs in the availability set, but not for the availability set itself.

## Common examples of Azure VMs
---
- Web servers: Host websites and web applications.
- Application servers: Run business logic and application code.
- Database servers: Host databases and manage data storage.
- Development and testing: Create isolated environments for development and testing.
- Disaster recovery: Use VMs as part of a disaster recovery strategy to ensure business continuity in case of failures.
- Extending your datacenter into the cloud: Use VMs to extend your on-premises datacenter into Azure, allowing you to take advantage of the scalability and flexibility of the cloud while maintaining control over your infrastructure. SharePoint, Exchange, and SQL Server are common examples of applications that can be run on Azure VMs as part of a hybrid cloud strategy.
- Lift and Shift migrations: Use VMs to migrate existing applications to Azure with minimal changes, allowing for a quicker transition to the cloud. However, running VMs in the cloud and not using microservices or serverless architecture may not be the most cost-effective solution in the long term, as it can lead to higher costs and maintenance overhead compared to more modern cloud-native approaches.

## Provisioning VMs in Azure
---
To provision a VM in Azure, you can use the Azure portal, Azure CLI, or Azure PowerShell. The process typically involves the following steps:
1. Choose an image: Select an image from the Azure Marketplace or create a custom image that includes the operating system and any pre-installed software you need.
2. Configure the VM: Specify the size of the VM, the region where it will be deployed, and any additional settings such as networking, storage, and security options.
3. Create the VM: Once you have configured the VM, you can create it by clicking the "Create" button in the Azure portal or using the appropriate command in Azure CLI or PowerShell. The VM will be provisioned and deployed to the specified region, and you can monitor its status and manage it using the Azure portal or command-line tools. After the VM is created, you can connect to it using Remote Desktop Protocol (RDP) for Windows VMs or Secure Shell (SSH) for Linux VMs to manage and configure the operating system and applications running on the VM. You can also use Azure Automation or Azure DevOps to automate the provisioning and configuration of VMs in Azure, allowing you to create and manage VMs at scale with minimal manual intervention. Additionally, you can use Azure Resource Manager templates to define the infrastructure and configuration of your VMs as code, making it easier to deploy and manage your VMs consistently across different environments.

# Exercise: Provision a VM in Azure
---
1. Log in to the Azure portal and navigate to the "Virtual Machines" service.
2. Click on the "Create" button to start the VM creation process.
3. Select an image from the Azure Marketplace or create a custom image that includes the operating system and any pre-installed software you need.
4. Configure the VM by specifying the size, region, and any additional settings such as networking, storage, and security options.
5. Click the "Create" button to provision the VM. Monitor the deployment process and wait for the VM to be created.
```powershell
az vm create --resource-group "IntroAzureRG" --name my-vm --size Standard_D2s_v5 --public-ip-sku Standard --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys
```
This command creates a VM named "my-vm" in the resource group "IntroAzureRG" with the specified size, image, and authentication method. The `--generate-ssh-keys` option creates SSH keys for secure access to the VM. You can monitor the deployment process in the Azure portal or using the Azure CLI. Once the VM is created, you can connect to it using SSH or RDP depending on the operating system you chose.
6. Install NGINX on the VM and configure it to serve a simple web page. You can use the following commands to install NGINX on an Ubuntu VM:
```powershell
az vm extension set --resource-group "IntroAzureRG" --vm-name my-vm --name customScript --publisher Microsoft.Azure.Extensions --version 2.1 --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```
This command uses the Custom Script Extension to run a script that installs NGINX on the VM. The script is hosted on GitHub and will be downloaded and executed on the VM. After the script runs, NGINX will be installed and configured to serve a simple web page. You can verify that NGINX is running by navigating to the public IP address of the VM in a web browser. You should see a default NGINX welcome page, indicating that the web server is up and running. You can also customize the web page by modifying the NGINX configuration files on the VM or by uploading your own HTML files to the appropriate directory on the VM. This exercise demonstrates how to provision a VM in Azure and use it to host a simple web application, showcasing the flexibility and power of Azure VMs for running a wide range of workloads and applications in the cloud.
7. Navigate to the IP of the machine and verify that the NGINX welcome page is displayed. You can find the public IP address of the VM in the Azure portal under the "Overview" section of the VM. Once you have the IP address, enter it into a web browser to access the NGINX welcome page. If you see the welcome page, it means that NGINX is successfully installed and running on your VM, and you can start customizing it to serve your own web content or applications as needed.
8. To clean up the resources you created, you can delete the VM and the resource group using the following commands:
```powershel
az vm delete --resource-group "IntroAzureRG" --name my-vm --yes
az group delete --name "IntroAzureRG" --yes --no-wait
```
This will delete the VM named "my-vm" and the resource group "IntroAzureRG" along with all the resources contained within it. The `--yes` flag confirms the deletion without prompting for confirmation, and the `--no-wait` flag allows the command to return immediately without waiting for the deletion to complete. Always ensure that you have backed up any important data before deleting resources, as this action is irreversible.

NOTE: You may need to use this machine again, either delete or recreate if you're using PAYG, Dupo. You're the FinOps guy, so save $ :)

# Describe Azure Virtual Desktop
---
Azure Virtual Desktop (AVD) is a cloud-based desktop and application virtualization service that allows users to access their desktops and applications from anywhere, on any device. AVD provides a secure and scalable environment for running virtual desktops and applications in the cloud, allowing organizations to provide remote access to their workforce while maintaining control over their data and applications. AVD supports both Windows 10 and Windows Server operating systems, and it can be used to host a wide range of applications, including Microsoft Office, line-of-business applications, and custom applications. AVD also integrates with other Azure services, such as Azure Active Directory and Azure Security Center, to provide enhanced security and management capabilities for virtual desktops and applications in the cloud.

Multisession on Windows 10 or 11 Enterprise allows multiple users to connect to the same vm. 

# Describe Azure Containers
---
Containers are a lightweight virtualization technology that allows you to package and run applications in a consistent environment across different platforms. Containers are best used to scale out and stop applications quickly. They are used for microservice architectures. These are more agile and faster to deploy than VMs. 

Docker is the most popular containerization platform. Azure allows you to run Docker containers in several ways, including:
* Azure Container Instances (ACI)
* Azure Container Apps
* Azure Kubernetes Service (AKS)
* Azure App Service. 
 
 ACI is a serverless container service that allows you to run containers without managing any infrastructure. 
 Azure Container Apps is a fully managed serverless container service that allows you to run microservices and containerized applications without managing any infrastructure.

The difference between Azure Container instances and Azure Container Apps is that ACI is a more basic service that allows you to run individual containers, while Azure Container Apps provides a more comprehensive platform for building and deploying microservices and containerized applications. Azure Container Apps includes features such as automatic scaling, built-in monitoring, and support for multiple programming languages and frameworks, making it easier to build and deploy complex applications in the cloud.

AKS is a managed Kubernetes service that provides a scalable and secure environment for running containerized applications. It is a more enterprise based fleet management solution for containers. It provides features such as automatic scaling, self-healing, and rolling updates, making it easier to manage and deploy containerized applications at scale. AKS also integrates with other Azure services, such as Azure Active Directory and Azure Monitor, to provide enhanced security and monitoring capabilities for your containerized applications.

Azure App Service allows you to deploy and run web applications in a fully managed environment, which can also support containerized applications. Each of these services provides different levels of control and scalability, allowing you to choose the best option for your specific use case and requirements.

No matter what you choose, Dupo, containers are used to run application pieces in microservices architecture. They are more agile and faster to deploy than VMs, and they can be easily scaled up or down based on demand. 

Imagine your website in multiple sections, backend, database, frontend, etc. Each of these sections can be run in a container, allowing you to scale each section independently based on demand. For example, if your website experiences a surge in traffic, you can easily scale up the frontend container to handle the increased load without affecting the backend or database containers. This allows for more efficient resource utilization and improved performance for your application.

# Describe Azure Functions
---
Azure Functions is an event driven, serverless compute option. VMs and Containers are always running, while Azure Functions only run when triggered by an event. This makes it a cost-effective option for running small pieces of code in response to events, such as changes to data in a database, messages in a queue, or HTTP requests. 

Azure Functions can be written in a variety of programming languages, including C#, JavaScript, Python, and PowerShell, and they can be easily integrated with other Azure services to create powerful and scalable applications in the cloud. Azure Functions is ideal for scenarios such as data processing, real-time stream processing, and building APIs or microservices that respond to events in real-time. 

Example: you can use Azure Functions to automatically process data when it is uploaded to Azure Blob Storage, or to trigger a workflow when a new message is added to an Azure Service Bus queue. This allows you to build highly scalable and responsive applications that can react to events in real-time without the need to manage any infrastructure. Azure Functions also provides features such as automatic scaling, built-in monitoring, and support for multiple programming languages and frameworks, making it easier to build and deploy complex applications in the cloud.

You only pay for the time that your function runs. 
Functions scale on demand, so you can handle any number of events without worrying about infrastructure.

Functions can be:
- Stateless: The default - Each function execution is independent and does not maintain any state between executions. This allows for easy scaling and high availability.
- Stateful: Durable Functions can maintain state between executions using durable functions, which allow you to create long-running workflows and manage state across multiple function executions. This is useful for scenarios such as orchestrating complex workflows, managing stateful applications, and handling long-running processes that require coordination between multiple function executions.
# Application Hosting Options
---
Azure provides several options for hosting applications, including Azure Web Apps, Azure Container Instances, and Azure Virtual Machines. 

Azure App Service lets you focus on building your application and Azure handles the environment, scaling and maintenance.

- HTTP based service
- REST APIs
- Web applications
- PHP, Python, JavaScript (Node.js), .NET, Java, and more
- Windows and Linux environments

App Service allows you to host app types such as
- Web Apps: Host web applications and APIs in a fully managed environment.
- Mobile Apps: Build and host mobile app backends with features like offline sync and push notifications. SDK support for iOS, Android, and React Native apps.
- API Apps: Host RESTful APIs with built-in support for Swagger and OpenAPI specifications.
- WebJobs: Run background tasks and scheduled jobs in a serverless environment.


Azure Web Apps is a fully managed platform for building and hosting web applications, while Azure Container Instances allows you to run containerized applications without managing any infrastructure. Azure Virtual Machines provide more control over the underlying infrastructure and are ideal for running applications that require specific configurations or dependencies. Each of these options has its own advantages and use cases, and the choice depends on the specific requirements of your application and your preferences for management and scalability.


# Describe Azure Virtual Networks
---
Azure Virtual Networks (VNet) are a fundamental building block of Azure's networking infrastructure. They provide a secure and isolated environment for your Azure resources, allowing you to control the flow of traffic between resources and the internet. A VNet is a logical representation of a network in Azure, and it can be segmented into subnets to further isolate resources. VNets can be connected to on-premises networks using VPN Gateway or ExpressRoute, allowing for hybrid cloud scenarios. VNets also support features such as network security groups, which allow you to control inbound and outbound traffic to your resources, and Azure Firewall, which provides centralized security and traffic filtering for your VNet. Overall, Azure Virtual Networks provide a flexible and secure way to connect and manage your Azure resources in the cloud.

- Isolation and Segmentation
- Internet Communications
- Communication with Azure resources and On Prem via VPN or ExpressRoute
- Network Security Groups and Azure Firewall for security and traffic filtering
- Route and filter traffic with Azure Firewall and NSGs
- Azure DNS for domain name resolution within the VNet

Supports both public and private endpoints, allowing you to control access to your resources and ensure secure communication between them. 
- Public endpoints allow resources to be accessed from the internet
- Private endpoints allow resources to be accessed only within the VNet or through a VPN connection. This allows you to create a secure and isolated environment for your Azure resources while still enabling communication with the outside world when necessary.

Isolation and segmentation: define an IP range that is only available to you. You can then divide that into subnets for further isolation.

Internet Communications: Assign a public IP address to a resource or create a public load balancer. 

Communicate between Azure Resources: Service Endpoints allow you to connect to Azure services privately over the Azure backbone network. The rest of the resources in the VNet can communicate with each other using private IP addresses. You can also use VNet peering to connect two VNets together, allowing resources in both VNets to communicate with each other as if they were on the same network.

Communicate with on-premises networks: Use VPN Gateway or ExpressRoute to connect your VNet to your on-premises network, allowing resources in the VNet to communicate with resources in your on-premises network.

Route Network Traffic: Use Azure Firewall and Network Security Groups (NSGs) to control the flow of traffic between resources in your VNet and the internet. You can create rules to allow or deny traffic based on source and destination IP addresses, ports, and protocols.
- Route Tables: allow you to control the routing of traffic within your VNet. You can create custom routes to direct traffic to specific destinations, such as a virtual appliance or a specific subnet. This allows you to control the flow of traffic within your VNet and ensure that it is routed correctly based on your specific requirements.
- Border Gateway Protocol (BGP): allows you to exchange routing information between your VNet and on-premises networks or other VNets. This is particularly useful when you have multiple VNets or on-premises networks that need to communicate with each other, as it allows for dynamic routing and failover capabilities.

Filter Network Traffic: Use Azure Firewall and NSGs to control the flow of traffic between resources in your VNet and the internet. You can create rules to allow or deny traffic based on source and destination IP addresses, ports, and protocols. This allows you to secure your VNet and protect your resources from unauthorized access.
- Network virtual appliances (NVAs): These are third-party virtual machines that provide additional security and traffic filtering capabilities for your VNet. NVAs can be used to inspect and filter traffic, block malicious traffic, and provide additional security features such as intrusion detection and prevention. You can deploy NVAs in your VNet to enhance the security of your network and protect your resources from threats.

VNET Peering: allows you to connect two VNets together, allowing resources in both VNets to communicate with each other as if they were on the same network. This is useful for scenarios where you want to connect resources in different VNets, such as when you have multiple environments (e.g., development, staging, production) or when you want to connect resources in different regions. VNet peering is a low-latency, high-bandwidth connection that allows for seamless communication between resources in the peered VNets.


# Exercise: Configure Network Access
---
1. Using the VM and the NGINX configuration, get the IP address of the VM and navigate to it in a web browser to verify that the NGINX welcome page is displayed.
2. On a separate machine outside of the Azure network, try to access the NGINX welcome page using the public IP address of the VM. This will fail. 
3. Examine the Network Security Group (NSG) rules associated with the VM's subnet or network interface. Identify the rule that is blocking inbound traffic to the VM. You can find the NSG rules in the Azure portal under the "Networking" section of the VM or its associated subnet. Look for any rules that deny inbound traffic on port 80 (HTTP) or port 443 (HTTPS), which are commonly used for web traffic. If you find such a rule, it is likely the reason why you cannot access the NGINX welcome page from outside the Azure network. You can modify the NSG rules to allow inbound traffic on the necessary ports to enable access to the NGINX welcome page from external sources.
4. To allow inbound traffic to the VM, you can create a new NSG rule that allows traffic on port 80 (HTTP) or port 443 (HTTPS). In the Azure portal, navigate to the NSG associated with the VM's subnet or network interface, and click on "Inbound security rules". Click on "Add" to create a new rule, and specify the following settings:
- Source: Any (or specify a specific IP range if you want to restrict access)
- Source port ranges: *
- Destination: Any (or specify the IP address of the VM if you want to restrict access)
- Destination port ranges: 80 (for HTTP) or 443 (for HTTPS)
- Protocol: TCP
- Action: Allow
- Priority: Set a priority value that is lower than any existing rules that deny traffic on the same ports (e.g., 100)
- Name: Provide a descriptive name for the rule (e.g., "Allow-HTTP-Inbound")
5. After creating the NSG rule, wait a few minutes for the changes to take effect, and then try accessing the NGINX welcome page again using the public IP address of the VM. You should now be able to access the welcome page from outside the Azure network, indicating that the NSG rule is allowing inbound traffic on the specified ports. Remember to remove or modify the NSG rule after testing to ensure that your VM remains secure and only allows necessary traffic.
6. Clean this up by deleting the Resource Group and all associated resources.
NOTE: To give you an idea of how to use this in a real-world scenario, you might create 2-3 VMs and have them all serving up a web page. You could then connect to each machine to load the same web page. This isn't a production ready solution, but it gives you an idea of how to use NSGs to control access to your VMs and ensure that only authorized traffic can reach your applications. Adding a load balancer in front of the VMs would allow you to distribute traffic across multiple instances and provide high availability for your application.

Further adding in an App Gateway would allow you to manage traffic to your web applications, providing features such as SSL termination, URL-based routing, and Web Application Firewall (WAF) capabilities. This would enhance the security and performance of your web applications while allowing you to scale them effectively.


# Describe Azure Virtual Private Networks
---
A VPN is an encrypted secure connection that creates a tunnel between two networks. This is uses over the public internet most of th etime. 

VPN Gateway: 
- Deployed in a dedicated subnet
- Supports both site-to-site (datacenter to Azure)
- and point-to-site (individual client to Azure) VPN connections
- Supports multiple VPN protocols, including IKEv2, OpenVPN, and SSTP

Policy Based or Route Based VPNS:
- Policy-based VPNs use static routing and are typically used for simple, point-to-site connections
- Route-based VPNs use dynamic routing and are more flexible, allowing for more complex network topologies and multiple connections. They are typically used for site-to-site connections and support features such as BGP routing and multiple tunnels.

When to use Route Based VPNs:
- When you need to connect multiple sites or have a complex network topology
- Multisite connections
- point to site connections
- ExpressRoute connections

## High availability scenarios
---
- Active/Standby: when one fails, the other takes over. This does take about 90 seconds to failover, so it is not ideal for all scenarios. You can use Azure Load Balancer to monitor the health of the VPN Gateway and automatically route traffic to the standby gateway if the primary gateway fails.
- Active/Active: Public IP address to both instances, then create tunnels to both instances. If one instance fails, the other instance can take over the traffic OR be used simultaneously.
- ExpressRoute failover: When ExpressRoute fails, the connections are routed temporarily through the VPN gateway.
- Zone Redundant Gateways: Deploy these into multiple availability zones within the same region to ensure high availability and resilience against zone failures. This configuration allows for automatic failover between zones, providing enhanced reliability for your VPN connections.


# ExpressRoute
---
ExpressRoute is a private, dedicated connection between your on-premises network and Azure. It provides a more secure and reliable connection than a VPN, as it does not traverse the public internet. ExpressRoute connections are established through a connectivity provider, and they can be configured to provide high bandwidth and low latency connections between your on-premises network and Azure. ExpressRoute is ideal for scenarios where you need a high-performance, secure connection to Azure, such as for data transfer, disaster recovery, or hybrid cloud scenarios. ExpressRoute also supports features such as private peering, which allows you to connect to Azure services privately over the ExpressRoute connection, and Microsoft peering, which allows you to connect to Microsoft services such as Office 365 and Dynamics 365 over the ExpressRoute connection.

ExpressRoute Circuit: A logical connection between your on-premises network and Azure. It is created through a connectivity provider and can be configured with specific bandwidth and routing options.

Benefits:
-connectivity to MS cloud services across all regions
- Global connectivity with ExpressRoute Global Reach, allowing you to connect your on-premises networks across different regions through the Microsoft backbone network.
- Dynamic routing between your network and Azure using Border Gateway Protocol (BGP), which allows for automatic failover and load balancing between multiple ExpressRoute circuits.
- Private peering: Connect to Azure services privately over the ExpressRoute connection, providing enhanced security and performance for your applications.
- Microsoft peering: Connect to Microsoft services such as Office 365 and Dynamics 365 over the ExpressRoute connection, allowing for improved performance and reliability when accessing these services.


Direct Access to:
- Azure services: Connect to Azure services such as Azure Storage, Azure SQL Database, and Azure Virtual Machines over the ExpressRoute connection, providing improved performance and security for your applications.
- Azure Cloud services: Connect to Azure services such as Azure Kubernetes Service (AKS), Azure App Service, and Azure Functions over the ExpressRoute connection, allowing for improved performance and reliability when accessing these services.
- Microsoft services: Connect to Microsoft services such as Office 365 and Dynamics 365 over the ExpressRoute connection, allowing for improved performance and reliability when accessing these services.

Global Connectivity: ExpressRoute Global Reach exchanges data across on-premise sites by connecting your ExpressRoute circuits together through the Microsoft backbone. 
Example: if you have two datacenters in two different countries, one in Europe and one in the US, you can connect both datacenters to Azure using ExpressRoute, and then use ExpressRoute Global Reach to connect the two datacenters together through the Microsoft backbone network.

Dynamic Routing: ExpressRoute uses BGP. BGP can be used to exchange routes between on prem and Azure.

Built in Redundancy: Each ExpressRoute circuit consists of two connections to the connectivity provider, providing built-in redundancy and failover capabilities. If one connection fails, traffic is automatically rerouted through the other connection, ensuring high availability for your applications. Additionally, you can configure multiple ExpressRoute circuits for even greater redundancy and load balancing across different regions or providers.

## ExpressRoute Connectivity Models
---
- CloudExchange colocation: Connect to Azure through a connectivity provider that has a presence in the same colocation facility as your on-premises network. This allows for low-latency, high-bandwidth connections to Azure.
- Point-to-point Ethernet: Connect to Azure through a point-to-point Ethernet connection provided by a connectivity provider. This option is suitable for organizations that require a dedicated connection to Azure without the need for a colocation facility.
- Any-to-any (IPVPN): Connect to Azure through a virtual private network (VPN) provided by a connectivity provider. This option is suitable for organizations that require a flexible connection to Azure that can be easily scaled up or down based on their needs. It allows for connectivity from multiple on-premises locations to Azure, providing a more flexible and scalable solution for organizations with distributed networks. 
- Directly from ExpressRoute sites: Connect to Azure directly at a peering location using ExpressRoute, without the need for a connectivity provider. This option is suitable for organizations that have a large on-premises network and require a high-bandwidth, low-latency connection to Azure.

Security Considerations:
- ExpressRoute is a private dedicated connection
- DNS, CRL, Azure Content Delivery are still accessed over the public internet, so you should use Azure Firewall or NSGs to control access to these services and ensure that only authorized traffic can reach them.
# Azure DNS
---
Records in Azure DNS are hosted on Azure's global network of name servers, which are distributed across multiple regions and availability zones. This ensures high availability and low latency for DNS queries. Azure DNS supports various types of DNS records, including A, AAAA, CNAME, MX, NS, PTR, SOA, SRV, and TXT records. 
You can manage your DNS records using the Azure portal, Azure CLI, or Azure PowerShell. Azure DNS also provides features such as traffic management and private DNS zones, allowing you to control the flow of traffic to your applications and services while keeping your internal resources secure.

Azure DNS is based on Azure Resource manager
- RBAC
- Activity logs and auditing
- Resource Locking
- Can manage DNS domains and records using Azure CLI, PowerShell, or the Azure portal.

Private DNS:
- Allows you to create and manage DNS zones and records that are only accessible within your Azure virtual network (VNet).
- Custom domain names in private networks rather than the public Azure DNS names.


Note: Azure DNS is not a domain registrar, so you will need to use a domain registrar to purchase and manage your domain names. Once you have registered your domain name, you can create DNS records in Azure DNS to point to your Azure resources, such as virtual machines, web apps, or load balancers. This allows you to use custom domain names for your applications and services hosted in Azure while leveraging the global availability and performance of Azure DNS.
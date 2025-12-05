11. Connectivity and Load Balancing
---

# Azure Load Balancer
---
Allows for distributed traffic coming inbound into the network. Allows for self healing and redirection of traffic away from a resource that has broken. 

- Can be public or private.
- Can also be used between tiers

Azure Load Balancer is Layer 4
- Is not aware of the type of traffic
- Does not handle scaling

![image.png](/.attachments/image-4babbed0-572a-4d6e-a3e7-1cb382927ab1.png)

## Components
---
- Frontend - public/private IP address
- Backend - VMs or a VM scale set that host instances of the solution
- Probe - THe thing that checks for healthy instances
  - make sure your NSG is not blocking your probe
- Rules - what are you sending where?

![image.png](/.attachments/image-0b383457-337d-4b9e-9de8-f779182c6d92.png)

# Demo - Configure Regional Load Balancing 
---
1. Set up two VMs using Visual Studio 2022 Community on Server 2022 with public IPs, no NSG
2. On the extension, add the powershell script that you can store in a storage account. 
3. Create a Load Balancer - regions, sku, type (public) matter. 
4. Create the frontend IP address (a new public address is needed)
5. Add the VMs to the backend pool
6. Add a health probe (either http or https)
7. Add a Load balancing rule. 
![image.png](/.attachments/image-3e89ce99-d0cf-426b-8564-df533d5a914d.png) 
8. Navigate to the frontend IP and notice what server you are on. Refresh a few times and you might get stuck on one server.
9. Shut down one server and then refresh the page again. You should be automatically load balanced to the running machine. 
## Cleanup
---
Delete all resources that you created.
- Public IP
- VMs
- LB
- NSG (if you did)
- VNet and Subnets
- RGs

# Application Gateway
---
Layer 7 Load Balancing instead of Layer 4 for a normal load balancer.
- knows how to use path based routing
- multi-site routing
- end to end encryption
- WAFs
- web app aware

## Components
---
- Frontend - public/private IP
- Backend - services that are either public or private - can be a bunch of resources, not just VMs
- listeners and settings
  - front: port, ssl, multisite
  - back: port, cookie affinity, draining
- Probes
- Rules - supports path based routing

![image.png](/.attachments/image-4e1399ed-188e-46f4-8dd6-19c6e2545026.png)

# Demo - Configure App Gateway and path based routing
---
1. Create two ACI's with a web app on them. 
2. Create an app gateway to the same region
3. Standard, Standard v2, WAF, WAF v2 are options
4. One instance - can do a zonal deployment
5. Deploy to an existing network
6. Ensure the NSG is not blocking any ports
7. Create a public IP address
8. Configure the backend - without adding the ACI's to it. 
- create an app-pool and a web-pool
![image.png](/.attachments/image-79662280-eca3-49e1-b89e-56703f6e4107.png)
9. Create a new listener for the front end
NOTE: A listener is how the app gateway's ingress traffic is handled. 
10. Add the backend settings
11. Add in the paths. 
![image.png](/.attachments/image-236ff1f1-07db-4c5f-a734-7cf504271c19.png)
12. Finish creating the app gateway
13. Navigate to the frontend IP address and you'll get a 502 error (bad gateway) because we didn't configure the backend pools yet.
14. Configure the backend pools for both app and web. 
- use either the fqdn or the IP addresses
15. Notice that if you browse across into the app section, it goes to a different host than the rest of the app. 

# Azure Traffic Manager
---
This is a DNS load balancer. You don't connect through this, you use this to point to where you connect to. 

Traffic flow:
![image.png](/.attachments/image-95eb5c9c-a1b9-479a-8c35-7fbdf457e42f.png)

## Components
---
Profile - app.trafficmanager.net
Endpoints - internet facing services over any protocol (Publicly Accessible)
Monitoring - health check and failover method
Routing
- priority - send traffic to the highest priority endpoints. 
- weighted - endpoints are based on weights
- performance - closest
- geographic - location based
- multivalue - all healthy endpoints
- subnet - specific endpoints

# Demo - Configure Traffic Manager
---
1. Deploy this into your Azure subscription. https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-aem-web.json
2. Select your parameters
3. Create a unique traffic manager (remember DNS)
4. Select weighted and then choose the backend resources
5. On the Endpoints tab, add in the two VM's that were deployed earlier.
6. Navigate to the TM endpoint - notice that it resolves via DNS
7. Run a nslookup on the app.trafficmanager.net endpoint

# Azure Front Door
---
Layer 7 service
Load balancing and distributing the solution across the globally distributed network. 
- Global Load Balancing using MS's global network
- Accelerated delivery - caching, compression, etc. 
- Secure Connectivity - WAF, bot protection, threat intelligence. 

Tiers:
- Standard
- Premium

![image.png](/.attachments/image-8b92ab6c-e400-48d6-996a-de812ea61a4e.png)

## Components
---
Frontdoor Profile
- Endpoint - unique entrypoint into your app
- Origin group - publicly accessible endpoints
- Routes - maps an endpoint to an origin group with protocol, path, domain, cache, etc. 

Routing flow:
![image.png](/.attachments/image-a2cda3f5-98a0-421d-943a-b6de2f229e56.png)

# Demo - Azure Front Door
---
1. Deploy this link: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-aem-web.json
2. You can click this again and set another region if you would like
3. Grab the public IP of one of the machines and test in a browser and repeat for the other VM
4. Create Azure Front Door service
5. Select Azure Front Door and quick create
![image.png](/.attachments/image-fe2ca989-e5ee-44fb-ae5c-dee0e752457b.png)
Note: This is a global service
6. Resource Group, Subscription, name, standard/premium
7. Set up the endpoint - the entrypoint into your global presence
8. Check the list of Origin Types
9. Select Public IP and the VM host name
10. Enable caching if you want to
11. WAF Policy empty
12. Create

![image.png](/.attachments/image-913080a3-51e5-46ea-8c92-a3ed2da74bea.png)

13. Browse into the Front Door Manager and look at the endpoint
![image.png](/.attachments/image-5627711d-b179-438f-b7e9-554b03e426bb.png)
14. Click on the origin group and you'll see one of the IPs
![image.png](/.attachments/image-55d400a1-60b9-466d-9f97-de47363e455b.png)
15. Add the other IP to this Origin Host list
16. Navigate to the Front Door endpoint

## Cleanup
---
Delete all of this stuff

# Case Study
---
Migrate to Europe from Australia
Solution:
![image.png](/.attachments/image-308194aa-e32f-4735-8335-041d7165fcad.png)







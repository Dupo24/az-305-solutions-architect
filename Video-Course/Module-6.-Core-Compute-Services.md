[[_TOC_]]
# Virtual Machines
---
Full control to the OS
Lift and shift

Lots of times, the OS disk can be moved around and reattached to a new machine. Resizing a machine does this. It detaches the OS disk and reattaches it to a new machine. 

VM, NIC and VNet all need to be in the same region. You cannot connect a VM in China to a NIC in Germany for example. 

![image.png](/.attachments/image-8ad7244b-1cfe-4307-9c8d-04a032423172.png)

# Demo - Create a VM
---
1. Create a vm
2. Notice options, quota, redeployment, etc. 
- quotas are there to give MS an idea of what your account will be able to spin up. You will need to request more quotas if you need more than what your subscription allows. 

# Virtual Machine Scale Sets
---
Load balanced sets of VMs that help alleviate single points of failure. 
Takes care of high availability.
Also scales up and down to adjust for usage. 
![image.png](/.attachments/image-e56f38de-5dcb-42e5-a7ab-0a150f202e26.png)
![image.png](/.attachments/image-b955ba2a-129e-4f47-8229-4a64049f9509.png)

Upgrade policy can be:
- Automatic
- Rolling
- Manual

Auto scale rules based on metrics
- scale up or down based on the CPU/Memory requirements
- min, max, default instance limits (default is used when Azure can't read the metric info)
- scheduled scaling - scaling at certain date and times. 

# Demo - Deploy a uniform VMSS
---
![image.png](/.attachments/image-c7523700-fd26-43eb-b82f-31239621b446.png)

When you make a change, such as run a script on the VMSS, you need to upgrade or sync the VMSS VMs. 

You can also set the OS's to automatically update as well, providing you with the ability to keep with the latest security and enhancements. 

# Demo - Creating and Managing a Flexible VMSS
---
Flexible means you can add VMs to the VMSS as needed. 
It also means that the VMs that are part of the scale set are actual VMs that you can manage yourself outside of the scale set. 
VMs need to be in the same resource group and in the same region. 

1. Create VMSS
2. Create VM and add to the VMSS - check your Load Balancer 
3. Check the cloud init script. 

Demo - Configuring VMSS Autoscale
---
- Predictive autoscaling
- Metric based autoscaling

![image.png](/.attachments/image-cfc405fb-bd2d-4cb5-b218-f682f3a4faf4.png)
![image.png](/.attachments/image-584ce571-7a7d-49f2-b2f7-a284fbccfc6e.png)

Can also take messages from a queue to determine load on the scale set. 
Fixed profiles take priority over repeating profiles
![image.png](/.attachments/image-8677d898-3ec2-4e72-941e-f90454406a9c.png)

1. Build VMSS
2. Configure Autoscaling
3. Download a cpu stress utility
4. Run the stress utility and see if the instance counts increase.
5. Stop the stress utility and you can see the instance counts decrease.
6. You can also view the history of the autoscaling. 

# Azure App Service
---
This is a platform as a service that replaces VMSS - you deploy your code and Microsoft manages all of the infrastructure. 

- Web, mobile, API apps
- Container apps - docker, windows and linux. 
- Static web apps
- Other apps - ASE, Function apps, Logic Apps

![image.png](/.attachments/image-4340e4f0-73eb-4f67-b0b5-c72ff9c9bc01.png)

![image.png](/.attachments/image-34a3c920-067b-4d2c-a906-1abdf3e983cc.png)

App Service Plan is the underlying infrastructure for the app service. 
The App is the code or runtime environment of the application running on the app service plan. 

![image.png](/.attachments/image-f682d8bb-d74a-433a-ae72-f44501b9b565.png)

# Demo - Create a Web App with Azure App Service
---
1. Create the App Service Plan (do this separately to understand these are two different resources.)

![image.png](/.attachments/image-9e4f5a91-dd00-4920-8139-64eaac9e2e4d.png)

2. Create a web app. 

![image.png](/.attachments/image-f039a88e-7e30-4943-8269-67a783a2a5f5.png)

3. Add your custom domain if needed

![image.png](/.attachments/image-1772dea2-22e8-4f8a-b290-32d0bbf0d65f.png)

# App Service Deployments
---
![image.png](/.attachments/image-e520235a-1209-47f9-a99f-f743c986b62c.png)
![image.png](/.attachments/image-b301fd8d-20c5-499c-bba9-9ea52c1d2295.png)

You can deploy the updated code to a staging deployment slot and then split the traffic between these slots, so that you can pilot users. It's a very quick way to test your application in live. 
![image.png](/.attachments/image-0e46740d-218c-4433-a80a-d3f21fa923f5.png)

# Demo - Deploy a web app
---
You can link this web app to some random code repository in git or ado and have the website automatically deploy.
![image.png](/.attachments/image-7556f7c3-bef9-4516-988e-14d606bdbf3c.png)
![image.png](/.attachments/image-25016bca-d6cb-4683-9166-47d65d6e9fc4.png)

# Demo - Update a Web App using Deployment Slots
---
Upgrade your plan to an S1 or a plan that contains deployment slots
Create a staging slot
![image.png](/.attachments/image-75d59314-7780-4fea-9cf6-9e039a5f2c1e.png)
Set up the code to deploy to that staging slot
Deploy a V2 version of the app to that slot
Set the percentage of both slots to 50% - you should be able to see v2 load half the refreshes in the browser

## Troubleshooting
---
IF you run into errors, make sure your production slot is set for the default git repo that your original code is on:
![image.png](/.attachments/image-c40c97b1-790d-4cf1-aadd-564d756c2c18.png)
 
And then make sure your staging slot is linked to the local git repository:
![image.png](/.attachments/image-dd4b084d-cb13-4997-9149-1036fea7dfb3.png)

# Azure Functions
---
Azure Functions is a "serverless" compute service you can use to host small pieces of code. This code will run in response to some trigger. It has simple connectivity to other Azure services (through something called "bindings").

You can see examples of triggers and bindings in this [article](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings?tabs=isolated-process%2Cpython-v2&pivots=programming-language-javascript).
The key differences of the app service plans: [(MS Documentation)](https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale#overview-of-plans).

![image.png](/.attachments/image-b0da05d4-5e51-4338-93db-dd5a66355de0.png)

Azure Functions run code in response to an event or trigger without worrying about servers

Hosting Options:
- Consumption - serverless
- Premium - run and bill continuously, VNet connectivity, more powerful plans. 
- Dedicated - App Service plan and scaling is managed entirely by you. 

Architecture:
- Function app - container for the function - hosting plan that hosts the function
- Function - the actual code

![image.png](/.attachments/image-0cf714ed-f4f9-4b29-a0ff-78bd70583734.png)

# Demo - Create Azure Functions
---
Create the function
Pass a message into the function

![image.png](/.attachments/image-66771c5f-1940-498f-aa73-30a3cc8d799b.png)

If it isn't found in the blob, you get a 404 error:
![image.png](/.attachments/image-ad47d239-4520-47d4-b0e7-ce92478594ca.png)

# App Service Environment - ASE
---
Basically an App Service Plan that is more isolated - secure, government, etc. 

Solves this problem:
![image.png](/.attachments/image-cd5eeefc-414e-4f05-955b-ef6e035ab3b0.png)

Key features:
- Network or virtualized isolation
- supports hypervisor isolation
- network isolation through VNet integration
- Resource limits available through isolated pricing sku

![image.png](/.attachments/image-3c83af1b-f663-4ce8-b39b-3d344db09d70.png)

# Demo - Create an app service environment
---
1. Create the ASE
![image.png](/.attachments/image-55c5711c-b082-4937-b92c-a18029b87a02.png)
2. Check the hosting:
![image.png](/.attachments/image-faddcda6-6280-4907-a6f5-85d476608f98.png)
3. Check the networking - create a new VNet if needed.
![image.png](/.attachments/image-7d15c0ec-4284-466c-83de-930c93054725.png)
4. Tag and deploy - may take an hour or more to provision the isolated infrastructure:
![image.png](/.attachments/image-508bc378-e968-45b0-8447-ac8577f491fa.png)

Once deployed:
![image.png](/.attachments/image-a67560a6-4b9c-40c3-97a0-4c69b6567b6c.png)

Basically now you can treat your ASE as a new region in the dropdown for your web app. 
![image.png](/.attachments/image-59397cde-41d1-420e-9b23-d0a2fe89423b.png)

Your plans will be a bit more expensive as well because of that isolated infrastructure. 

# Case Study
---
![image.png](/.attachments/image-6e302fa3-112c-4484-b56b-9b932747de90.png)


Resources built for this module:
![image.png](/.attachments/image-daf06ae3-0be2-4fd0-9066-04a0a98c125d.png)



















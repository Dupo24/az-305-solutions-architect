[[_TOC_]]
# Essentials
---
Subscriptions are tied to one and only one Entra ID Tenant
![image.png](/.attachments/image-86a6b445-72c9-438d-913c-bb2a7429f9d2.png)
Extended features:
![image.png](/.attachments/image-0359d65b-553b-430b-b23d-516465a0a2aa.png)

## Entra ID Licensing
---
![image.png](/.attachments/image-f4ac157a-08a8-4076-b02f-8284e275c563.png)

## Managing Entra ID
---
3 ways:
- portal.azure.com
- entra.microsoft.com
- admin.microsoft.com

# Free subscription
---
Sometimes you can get a dev account or a free subscription that will give you credit for a month or so to learn. You can turn on trials for a month or so. 

# Additional Tenants
---
You need a paid Entra ID tenant to create additional tenants. 

## Subscriptions
---
When you click on a subscription, you will see on the Overview page the directory that the subscription is associated with.

Non Prod: 
![image.png](/.attachments/image-e25d985b-4cbc-4812-8841-9b41ddb6ba8a.png)

Production:
![image.png](/.attachments/image-d9e0abe4-09d6-4c3b-a715-eef17972b320.png)

## Budgets
---
![image.png](/.attachments/image-eb4ca40a-c708-403d-beb9-532753c6c708.png)

## Domains
---
You start out with something like in the screenshots above (dupo24msn@onmicrosoft.com) and can use your own domain as shown below:
![image.png](/.attachments/image-7f7fc792-7893-4b04-a377-286356d583cd.png)

You will need to own your own domain and then enter in a txt record to prove that you own that domain name. 

# Entra ID User Identities
---
Users are a type of identity within Entra ID

If all you have are Users in Entra ID, you have cloud identities.
Entra ID - User Identities
Active Directory synched - sychronized identities
Google, Facebook - guest identities

![image.png](/.attachments/image-816eab98-fedc-4e2f-90f7-4b2550ba3fb1.png)

## Deletion
---
Recycle bin type deletion - soft delete

## Bulk Actions
---
- Create
- Invite
- Delete

You get a CSV template to fill out and can upload

# Entra ID Application Identities
---
Human users aren't the only things that need access. Applications need access too. 
Applications are then authenticated and then after authentication, are authorized to access resources (SQL, VMs).

The application might need access to Entra ID or Users in our Entra ID might need to access the application as well.  

The application can then authenticate via a secret or via a certificate. 

# Demo: Register an Application in Entra ID
---
Create an app registration
Create a secret and copy it. 
Under the authentication tab, there is an option for Supported Account Types, which allows this application to be uses across other Entra ID tenants or your own single Entra ID tenant. 

## API Permissions
---
These allow the application to work with certain services and APIs:  
![image.png](/.attachments/image-c7ef2299-8757-4e38-b7eb-ec1a3cbacbab.png)

## Differences between app registration and Enterprise Application
---
Enterprise applications makes your app registration an entity that users can access. 
Who can access and how they can access it. 
Accessed through myapps.microsoft.com.

# Managed Identities
---
What is a managed identity?
If an application is hosted in Azure, you can use an appreg or app identity, but you'll need to provide a client id and secret or certificate.

IF the resource exists in Azure, use managed identities instead.  

Microsoft can manage the credentials on resources in Azure with Entra ID with a managed identity. 

- System assigned - single Azure resource - vm01 - once that vm is removed, the system assigned identity is removed.
- user assigned - multiple Azure resources - can be used on vm01, vm02, vm03, and when you remove vm01 and create vm04, the identity persists

# Demo Configure a System Managed identity
---
Run this link: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-generic.json

Build those resources

You will be deploying a VM and a system assigned managed identity to manage that resource. 

1. Browse to the machine
2. Go to Identity on the VM and toggle the system managed identity to ON.
![image.png](/.attachments/image-b0ad23c2-20da-45b4-98dc-dfa404686f0f.png)

3. Go to your app reg you created (Solos 305 App) and create a new secret
4. Add a reader role to the RG your resources were created in:  
![image.png](/.attachments/image-4505a3a4-fbd4-4138-ac46-6a9b23aeefde.png)

5. Log into the VM and open up powershell
6. run `az login --service-principal -u <clientid> -p <secret> -tenant <tenantid>`
7. This will allow you to log in using the app registration, but you're passing in a username and password
8. Run `az login --identity` and notice that this works the same without the client id and secret via the managed identity. 
9. Delete the RG to clean up. 

# Demo: Create a managed identity
---
Run this link: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-generic.json

Build those resources, select two VMs instead of one

You will be deploying two VMs and a user assigned managed identity to manage those resources. 

1. Search for managed identity and create.
2. Navigate to the machine, and add the managed identity. 

![image.png](/.attachments/image-1f256536-250e-453f-80bf-c7495ae2ee3d.png)

3. You can then add this to the other machine - or as many machines as you need to.
4. Deleting a machine doesn't delete the managed identity. 
You can then add the role assignment to this managed identity - like if you want that managed identity to access an entire subscription. 

# Entra ID Groups
---
- Reduce administrative tasks - you can add groups with permissions rather than individual users. 
![image.png](/.attachments/image-b117a338-ffb9-4d53-ae5d-067ef826c668.png)

- Self service capabilities - the leader of the team can be the owner and can manage their own membership to that group. 

- You can also use dynamic user groups to build groups based on common attributes such as location, etc. 
- additional features such as expiration, sensitivity labels
- members can be assigned manually or by the Entra with dynamic groups

![image.png](/.attachments/image-b8cb4837-c6a6-494e-886b-a47361db5faa.png)

# Demo: Creating a group
---
You can create a security group or a M365 group
Add a group, add an owner, add members
Check your expiration settings, set up an email, etc.

# Demo: Entra ID Licensing
---
Can be provisioned in Azure or in the Office portal
Licenses can fail because of missing attributes on the users such as location. 
Can assign licenses to users or groups. 
Reprocess in case license provisioning is failing. 

# Entra ID Dynamic Groups
---
Requires P1 Licensing
A dynamic group can be created based on a membership rule. (user.department -eq "Marketing") for example
Can be for devices or users but not both
Cannot manually add a user to a group that is dynamic. 
![image.png](/.attachments/image-27d4f81f-eca2-4f7c-b74c-f28745258d95.png)
Can validate users
This flattens out a group - can add multiple groups to avoid nesting issues. 

# Entra ID Administrative Units - AU's
---
The problem:
![image.png](/.attachments/image-7593845a-34f5-4dba-86c1-958c4a777d58.png)

The solution:
![image.png](/.attachments/image-379f93cc-367f-4756-8a9c-e16c83a08177.png)

- Can include a mix of users, group or devices
- membership can be assigned or dynamic
- you can have objects exist in multiple AUs at the same time
- Permissions do not apply to the individual membors
- Cannot have nested AUs within other AUs
## Restricted Management AUs
---
Denies administration to certain users or groups
![image.png](/.attachments/image-4cc11be2-c8f0-4b44-8240-5b187d48d489.png)

# Demo: Administrative Units
---
![image.png](/.attachments/image-fd0a1d49-1cb8-47fb-b5f0-e27fc3c1ecd0.png)

# Case Study
---
![image.png](/.attachments/image-679fd996-74de-467a-b61c-2a61d5139e3a.png)


























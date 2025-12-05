[[_TOC_]]
# Azure Role Based Access Control
---
![image.png](/.attachments/image-c3d270da-93fb-4239-905c-e764bd1fc13f.png)
A role definition is what sets of permissions that you have in an Azure subscription.

Utilizes all of the identities, user, device, managed, group identities. 

Contributor = can do pretty much everything except manage roles. 
These roles are only for management plane operations, not data plane operations.
Example: You need special access to key vault access controls (usually the role has Data in the name)
Custom Roles: Custom permissions for specific roles not already in Azure's list of existing roles.
Scope: You can apply those roles to specific scopes, Management groups, subscription, RG level or individual resource. 
![image.png](/.attachments/image-3113a45a-9412-4064-9fda-b4f695233ef3.png)

# Demo: Manage Azure Resource Security with RBAC
---
1. Deploy VM from the link: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-generic.json

2. Stop the VM. - you have seen permissions in action - why does your account have the ability to create and stop resources? Owner permissions on the subscription/organization. 

3. Assign some permissions to a user and then try to log in as that user
4. Try doing things that you have the permissions for, and try doing things that you DON'T have permissions for.

Note: there is no explicit deny - if the user doesn't have the perms, they don't get to do. 

# Entra ID Roles
---
These are specific permissions to Entra ID
- create users
- reset passwords
- register, delete, disable devices

![image.png](/.attachments/image-4603f028-80ce-4dc0-9219-fbbcd620a721.png)

Use Least Privilege access
- Helpdesk team gets what permissions? Not Global Admin perms
- Network team gets what permissions?
- Platform team gets what permission?

# Demo - Manage Entra ID Permissions
---
1. Click on Roles and administrators - these are Entra ID permissions, not resource access permissions, so you won't see anything for virtual machines or storage accounts here. 

You can scope these to the entire directory or to specific administrative units. 
You can assign roles to groups, but the groups need to be role-assignable. You cannot change the role assignable once the group is created.

# Azure RBAC Custom Roles
---
You create a role definition
- Metadata consisting of name, description, etc
- Permissions for managment and/or data plane operations
- Scope - where can the role be used at?

Permissions:
- Actions - allowed control plane actions
- NotActions - not allowed control plane actions
- DataActions - allowed data plane actions
- NotDataActions - not allowed data plane actions

You don't need to explicitly tell Azure to deny permissions. Not actions are subtracting permissions from the Allowed.
![image.png](/.attachments/image-584a8a7d-8561-4500-a15f-250d781213af.png)

Scope:
Assignable scopes
- root
- management groups
- subscriptions
- resource groups

Need to assign them as follows:
![image.png](/.attachments/image-08ac7d9f-df2d-4b89-95a5-8afaf0fdcf9d.png)

# Demo - Configure a custom RBAC role
---
Create a custom JSON, apply it to the role, assign the role to the group as usual. You can do this via powershell or via the portal. 
- Create a new folder: `mkdir roles`
- Navigate to the folder: `cd roles`
- Create/edit the role definition: `code koalaficationTeam.json` 
- Create the role: `New-AzRoleDefinition -InputFile ./koalaficationTeam.json`

# Entra ID Custom Roles
---
Starts with microsoft.directory
Premium P1 licensing
- Using Powershell or Graph API provides more control over the role definition

Need Global Admin or Privileged Role Admin permissions to create custom Entra ID roles. 

# Demo - Configure a Custom Entra ID Role
---
This is done within Entra ID -> Roles and administrators -> create role

This is for microsoft.directory and only for Entra ID, not for Azure resources. 

# Case Study - Design IAM
---
![image.png](/.attachments/image-958d9d37-933f-4aed-b732-0b3e720d32bf.png)

























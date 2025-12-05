[[_TOC_]]
# Entra Connect
---
Used to sync between AD and Entra ID

Two sync service tools:
- Entra Connect Sync
- Entra Connect Cloud Sync

Additional tool called Entra Connect Health.

![image.png](/.attachments/image-e559c2ad-4c7c-4161-873e-a4e5397ea2d6.png)

![image.png](/.attachments/image-4fde8419-01c8-42ca-8244-93f0bfce1f83.png)

# Entra Domain Services
---
If you need some support for legacy AD domain services, you can build out a cloud based AD instead of deploying your own domain. 

You can then connect Entra ID to your on prem via Entra Connect. 

![image.png](/.attachments/image-f5674e00-9d81-427a-854b-10bd1ceb2b9e.png)

# Entra ID External Identities
---
Business to business collaboration - B2B - access to our resources from another tenant or another identity provider. 

We can invite the guest user and that user can then accept that invitation to our tenant. 

![image.png](/.attachments/image-19d1530e-51e9-46a6-94e7-51ed61bf71ba.png)

B2B Direct Connect - Teams integration - Trusted organization with another Entra ID tenant. 

Business to consumer - B2C - identity for an app YOU are developing. 

![image.png](/.attachments/image-75ad01b6-fb8f-4176-9d74-5a7efa0ed549.png)

# Demo - Invite a guest with B2B Collaboration
---
Create a test user in one tenant
Invite the user from the other tenant
Redeem the invitation from the test user
Sign in and view from the test user cross tenant. 

Remember you are creating a guest identity in your tenant that the external user can use.

# Demo - Configure B2B collaboration with Google
---
![image.png](/.attachments/image-1f279455-b900-42c2-9fa6-ccb59fa593fe.png)

In Google:
![image.png](/.attachments/image-af0573a0-032f-45cd-9e38-1489b95825ff.png)
Email invite:
![image.png](/.attachments/image-66087628-56be-4fda-b072-ddeff4a39bce.png)
![image.png](/.attachments/image-57c90e76-e521-4b82-8d5b-527ab90f8e4a.png)
![image.png](/.attachments/image-ad4b40ab-9210-46db-9d18-c97c1b00047f.png)

# Entra ID Governance Overview
---
- Entitlement management - access managment
- Privileged Identity Management - PIM - JIT access
- Access Reviews - scheduled checks
- Lifecycle Workflows - Joining, moving, leaving
- Terms of use - Usage policies, acceptance and consent. 

![image.png](/.attachments/image-dc28a81a-8c97-4995-bd2c-9e862565a536.png)

Licensing required:
![image.png](/.attachments/image-ed759125-9ea3-4070-a0aa-39e3b297b4ab.png)

# Entra ID Entitlement Management
---
- https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-overview#license-requirements

- https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-delegate#entitlement-management-roles

Simplifies how entitlement is managed at scale. 

![image.png](/.attachments/image-eb538222-f904-4ba3-bd3d-056409b7bf6e.png)

Licensed feature: Identity Governance license
- Licenses are required for those who review, request, assigned a package
- Access packages are created in the portal. Managed via myaccess.microsoft.com
- Permissions: Identity Gov Admin, Access Package Manager

Terms:
![image.png](/.attachments/image-2fb319fc-267a-4c36-81ed-ab7e64a502df.png)

Roles and responsibilities:
![image.png](/.attachments/image-0e3f77cd-f49e-4ab3-ae02-a1906959db37.png)

# Demo - Create and use an access package
---
Need to watch that video again - we don't use this

# Entra ID Privileged Identity Management (PIM)
---
Just in time access for permissions

![image.png](/.attachments/image-9ccfbaa0-532f-4ffe-91d4-6931fb58ba57.png)

- Identity - eligible for permissions
- Assignment - active or eligible
- Activation - request to turn those permissions on, can have approvals, MFA. 

# Demo - Entra ID PIM
---
- Eligible
- Active
- Expired

Can activate with or without approval, add ticket number, justification, etc.
Can also deactivate the role if needed. 

# Entra ID Access Reviews
---
Over time, loose permissions linger on users as they move through projects or teams. Access Reviews assist with the lifecycle management of these permissions. 
![image.png](/.attachments/image-05284840-557c-4ada-90c2-2fc07b0da1e1.png)

- Teams and groups - user membership reviews
- applications - internal and guest user reviews
- Azure RBAC - PIM - active and eligible
- Entra ID - PIM - active and eligible

Access reviews are the ability to regularly conduct reviews and allow the users and their leaders to verify whether the access is still needed. 

# Demo - Create and run an access review
---
1. Add user to a role
2. Create an access review on the role that you added the user to. 
![image.png](/.attachments/image-fc37921f-239c-4836-b03e-da9e9741e7ae.png)
3. Self service? 
- Members(self) might be a good option
- Manager might be another good option. 
- Manually selecting a reviewer might be another good one. 
4. Click Start
5. log in as the user that you want to perform the access review on. 
6. Perform the self review as the user
7. View the results of the review

# Entra ID Protection
---
Entra ID Protection analyzes signals relating to your identities, and measures whether there is any risk (low, medium, or high). In this lesson you'll learn what sort of risks are being identified, and the policies you can configure in ID Protection.

This is only to protect the identity itself, not the resources

Three different types of policies
- Sign in Risk Policy
- User Risk Policy
- MFA Registration Policy - enforce MFA
![image.png](/.attachments/image-5c24f0bf-0912-497d-9b40-02e844e08934.png)

![image.png](/.attachments/image-c0796cc0-215a-4b06-ad84-65e1c32adffd.png)

These policies are configured at the tenant level - you can only have one policy of each type configured. 
You can get greater reporting when using this in conjunction with Conditional Access Policies

# Demo - Explore ID Protection Policies
---
![image.png](/.attachments/image-4c3f9e3b-1f3c-45c5-ac9d-3c005624886f.png)
Conditional Access is preferred over User Risk policy
Risks - https://learn.microsoft.com/en-au/entra/id-protection/concept-identity-protection-risks

Weekly digest might be of some importance:
![image.png](/.attachments/image-11a25898-fba0-4104-8c39-bd7accca094c.png)

# Entra ID Conditional Access
---
![image.png](/.attachments/image-517c14f7-5e11-4b20-91d2-c9ba854f691b.png)

Identities get access to resources WHEN conditions are met. 
- Risk
- Location
- Device Platform
![image.png](/.attachments/image-bc9522d8-b327-48b7-af2a-d6e5f740c543.png)

# Demo - Configure Conditional Access Policies
---
Be careful not to create a Conditional Access Policy which locks you out of the Azure Portal :)

![image.png](/.attachments/image-caca1c07-9f1b-41d2-a63e-cb05c2dde046.png)

1. Disable the security defaults: 
![image.png](/.attachments/image-4e7aa408-0e73-4ced-94c4-3de33b30400a.png)

1. Name the policy
2. Select the users to include - all users
NOTE: EXCLUDE YOUR MANAGEMENT ACCOUNTS - such as global administrator roles -  SO YOU DON'T GET LOCKED OUT
3. Select the application you want to restrict access to - this is to demonstrate without selecting all of Azure. 

4. Select conditions:
![image.png](/.attachments/image-a2eaca22-e947-4c71-ac43-bce2e06d0b50.png)
5. Select your grant options:
![image.png](/.attachments/image-d69b5d7d-b42a-4f8b-bee6-117ea383ac78.png)

## Whatif section
---
![image.png](/.attachments/image-a5248daa-e576-480b-88c9-96befc11adb3.png)

# Entra ID Self-Service Password Reset (SSPR)
---
Allows the user to self reset their own password. 

1. Enable this for the tenant
2. Auth methods configured for SSPR
3. Users Registration

![image.png](/.attachments/image-5f93749b-fe7f-43d6-b4a7-fdc4dade30a6.png)

#  Demo - Configure SSPR
---
![image.png](/.attachments/image-5aa5397e-f9dc-4e5d-968e-348add9e02c7.png)

![image.png](/.attachments/image-87b1d18a-752f-4362-b9e1-b6b61225cb47.png)
Security Questions:


Register:
![image.png](/.attachments/image-0e9c8476-73bd-403f-85d0-905bbaa22996.png)

Password Writeback:
Used if you have Entra ID Connect

![image.png](/.attachments/image-0bc3cb0f-ac41-479d-9dae-4271095bf7cc.png)

# Entra ID App Proxy
---
![image.png](/.attachments/image-9d58d6e0-97dd-4724-a9b1-03a707685efa.png)

Supported protocols:
Integrated windows auth

Components:
![image.png](/.attachments/image-f25c8119-91c1-48aa-a1ba-3f2d854b6365.png)
Auth Flow:
![image.png](/.attachments/image-313de08d-47c2-4e55-b4e1-84db72d7ed73.png)

# Demo - Configure Entra ID App Proxy for a Web App
---
You will need a P1 license here
You are going to pretend that the VM is On Prem
---

1. Deploy the template from here: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-generic.json
2. Go to the public IP and the site should load in your browser. 
2. Delete the access via HTTPS via the NSG that says to allow the inbound HTTP
4. RDP into the machine
5. Inside the machine, log into Entra ID and click on the Application Proxy option on the left
6. Register a new application registration - this will also create an Enterprise Application
7. Enabled for sign in, assignment required is disabled, allowed for all users in the Ent App properties,
8. Go into the Application Proxy section and fill in the details - make sure you select the correct connector environment.
9. Navigate to the fqdn for the app proxy and it should take you to the website. 

# Case Study - Design Extended Identity Services
---
Entra P1 Licensing required
Moving from off premise to the cloud, looking to decom the rest of it. 

Question:
How would you provide access to the existing application while decomming the infrastructure?

Solution:
Create App Proxy to the application
Configure conditional access policies
upgrade to premium P2 licensing to support this























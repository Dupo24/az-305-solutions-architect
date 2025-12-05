# Key Vault
---
These are used to secure all of the SSL certs, keys, secrets, etc for your application to use. 

![image.png](/.attachments/image-e977bdce-0421-4f59-befe-7a3b7ab1d920.png)

Higher tier will give you a HSM on top of the normal security. 

Everything is stored on the Data plane, management and users are configured on the Management plane

![image.png](/.attachments/image-39592484-3dc0-4811-9238-2e477887cddd.png)

1. You will need to create an access policy to give access to the data plane...or
2. Use Azure RBAC on the data plane. 

## Considerations
---
- Only can be accessed via a Entra ID identity
- Managed identities are recommended for apps (vs app reg and secret)
- Protect data with Soft delete (recycle bin) and Purge Protection (time based lock)

# Demo: Create, Configure and Use a Key vault
---
1. Deploy this link: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-acr-dockervm.json
- this will create an ACR, a VM and some related infrastructure
2. Create the Keyvault
- set purge protection to off and the soft delete to 7 days.
- RBAC access policy - the one that is recommended
3.  On the VM, create a system assigned managed identity
4. On the KV, go to secrets - you will be unauthorized - this is because you haven't assigned RBAC on the data plane.
![image.png](/.attachments/image-4af3502d-bde6-4dc2-9fda-ef943b2e09d7.png)
5. Add your user to the IAM Access Control and you'll be able to access.
6. Add your ACR access key to the KV as acr-password
7. Add the VM's managed identity as a KV Secrets User role assignment
8. Log into the VM via Public IP
9. Log in using that managed identity
10. Retrieve the KV secret using the commands below
11. Logout of Azure.
12. Log in using Docker using the command below.
## Commands:
---
*   Login to Azure: `az login --identity`
*   Create a variable for ACR name: `acr="youracrname"`
*   Create a variable for Key Vault name: `vault="yourkvname"`
*   Retrieve the password: az keyvault secret show --name acr-password --vault-name $vault --query value -o tsv
*   Assign password to variable: `password=$(az keyvault secret show --name acr-password --vault-name $vault --query value -o tsv)`
*   Logout of Azure: `az logout`
*   Optional docker login: `docker login $acr.azurecr.io --username $acr --password $password`

# Demo: Push a Container to ACR using a KV Secret
---
1. Do the previous demo
2. Log into the VM
3. Pull down the repo
4. Create a docker image and tag the image with the ACR details: `docker build -t $acr.azurecr.io/webstore:latest -f Dockerfile .`
5. Push this to the container registry: `docker push $acr.azurecr.io/webstore:latest`
6. Create a new Container Instance, and attach the ARC and the image.
7. Set up the public networking on port 80. 
8. Access the IP address via browser :)

Note: As a bonus, automate the ^ by using a script. 

# Entra ID Permission and Consent
---
![image.png](/.attachments/image-f34e5610-882e-4770-8947-a8e91ce3a151.png)

You can either work as the app or work as the user - remember this:
![image.png](/.attachments/image-10e3c0ae-c04c-4cb3-a2fe-c5315f224921.png)

## Key components:
---
App Registration - apps wanting to authenticate via Entra ID to access a resource
API Registration - the Web API that exposes its features/data viea Entra ID
API Permissions - Actions the API allows to be performed - Delegated or Application

![image.png](/.attachments/image-c50d57c5-edbf-44c8-99e2-2e0e3a28408f.png)

# Demo: Configure an app with Delegated Permissions
---
1. Deploy this link here: https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamesdplee%2Fcloudlee-click2deploy%2Fmain%2Ftemplates%2Fvm-devtools.json
2. Clone down the repo
3. Open the dir in VScode
4. Enter in these commands:
```
py -m venv .venv
.venv\scripts\activate
py -m pip install -r requirements.txt
```

5. Create a .env file, entering in your client ID and secret:
```
# Note: If you are using Azure App Service, go to your app's Configuration,
# and then set the following values into your app's "Application settings".

CLIENT_ID=YOURID
CLIENT_SECRET=YOURSECRET

# The AUTHORITY variable expects a full authority URL.
#
# If you are using an AAD tenent, configure it as
# "https://login.microsoftonline.com/TENANT_GUID"
# or "https://login.microsoftonline.com/subdomain.onmicrosoft.com".
#
# If you are using a CIAM tenant, configure it as "https://subdomain.ciamlogin.com"
#
# Alternatively, leave it undefined if you are building a multi-tenant app in world-wide cloud
AUTHORITY="https://login.microsoftonline.com/YOURDOMAIN.onmicrosoft.com"
```
6. You don't have a client ID or secret, so we'll need to set that up
7. Go into Entra ID and register an application.
8. Copy the Client ID and create a new Secret and paste it in the .env file. 
9. Run the app: `py -m flask run --debug --host=localhost --port=8000`
10. Sign in as a user and realize it needs a permission
11. Add the API permissions - delegated and add in User.readwrite.all and then consent to the use as an administrator.
12. Log in again.
13. Notice that if you don't have the permissions as a user, you won't be able to do what you're allowed to do. 

# Demo: Configure an app with App Permissions
---
1. Complete the previous demo, but delete the delegated permissions on the API permissions tab. 
2. Add in the application permissions
3. Notice you don't need to log in and you'll be able to do whatever the app needs it to do

## Cleanup
---
Delete the app registrations. 

# Case Study
---
![image.png](/.attachments/image-8cc167e9-d103-4cbb-a3b3-4605f2d738df.png)

















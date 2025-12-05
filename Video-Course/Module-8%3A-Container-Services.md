[[_TOC_]]

# Azure Container Registry
---
Why do we need these?
We have a Dockerfile - the source of all of our application dependencies and code and need to put it someplace so that something else can grab it and run it. 

![image.png](/.attachments/image-9d318094-dc4a-42b3-864e-90e9116e15df.png)

Features:
- Container Storage and Azure AD integration
- More storage
- VNet security, geo-replication, content trust

ACR Tasks provide some automation around the ACR

## Hierarchy
---
1. Registry - IAM, networking, pricing
2. Repository - where the images are stored
3. Artifacts - Helm

# Demo: Create a Container Registry and Push a Container
---
1. Clone a repo
2. Build the image
3. List the image
4. Create ACR
5. Create Repository
6. Push image to the repository
## Commands
---
*   Clone the repo: `git clone [https://github.com/org/repo.git]`
*   Build the docker image: `docker build -t appname -f Dockerfile .`
*   List docker images: docker image ls
*   Login to Azure: `az login`
*   Login to ACR: `az acr login -n registryname`
*   Tag image for ACR: `docker -t appname registryname.azurecr.io/appname:v1`
*   Push image to ACR: `docker push registryname/azurecr.io/appname:v1`

# Demo: Push an image with ACR tasks
---
This one uses Azure CloudShell

*   Make a new folder in Cloud Shell: `mkdir dev`
*   Change to new folder: `cd dev`
*   Clone the repo: `git clone https://github.com/org/repo.git`
*   Change to dev/appname folder: `cd appname`
*   Build and push: `az acr build --image acrtasks/appname:v1 --registry registryname --file Dockerfile .`

# Azure Container Instances
---

![image.png](/.attachments/image-8e3b022b-f1d9-424a-8ea1-f4ec05b5b045.png)

- Doesn't include scaling, healing, orchestration
- Pricing is based on resource allocation
- For simple solutions

## Hierarchy
---
Container Instance
Connectivity - public or VNet, DNS
Persistent storage via Azure Files

plus....
Container Groups
Hosting
![image.png](/.attachments/image-854697e6-f2db-4793-beb9-4e8d3408da85.png)

# Demo: Create an Azure Container Instance
---
1. Turn on the Access Keys on the ACR
2. In real life, use RBAC.
3. Navigate to Container Instances and Create a new instance
4. Check the zonal deployments
5. Select the image
6. Configure networking
 - private or public
7. Set the DNS label
8. Select the ports for your app - 443 or 80 or whatever
9. Restart Policy - restarts on failure or always or never
10. Look at encryption options
11. Environment Variables are sometimes needed
12. Click Create
13. Check the metrics, logs, and then copy the FQDN to a browser and see if the site is up. 

# Azure Kubernetes Service - AKS
---
Built by Google to host their own solutions. 

- Discovery and Load Balancing
- Automation
- Healing
- Scaling

![image.png](/.attachments/image-006e4bb7-5e67-4448-8acb-744aeee45185.png) 

Considerations:
- Entra ID
- Supports VMs and ACS
- Orchestration, healing, monitoring
- Only pay for the compute, not the control plane. 

Hierarchy
- Containers
- Clusters - API, etcd, scheduler, controller manager
  - Node pool - contains nodes (the VMs)
- Deploy - command line tools (kubectl)
- Pods - Deployments (YAML Manifest)

![image.png](/.attachments/image-ec2cc333-054e-49dc-9024-fe1600931312.png)

# AKS Networking
---
- Kubenet - network to pods via nodes
  - special CIDRs
- Azure CNI - pods connect to VNet
  - Each pod gets an IP from your network. 

## Services
---
Services are created in a Service CIDR

Cluster IP:
- Exports the service on a cluster service IP - Internal Only
![image.png](/.attachments/image-616644f9-0634-44be-9405-6509cc8bbb1a.png)

NodePort
- Exposes the service on a fixed port via the node IP - port translation
![image.png](/.attachments/image-16bec714-cdee-4794-88a5-7ae2857818dd.png)

Load Balancer
- Exposes the service via an Azure Load Balancer
![image.png](/.attachments/image-d25d04c3-aa96-4983-97e5-6a800e78b44d.png)

ExternalName
- Provides DNS for the service

## Network Policies
---
- Azure NPM (Network Policy Manager)- supports Azure CNI only
- Calico - supports Azure CNI and Kubenet

# Demo: Create and manage an AKS Cluster
---
1. Navigate to Azure Kubernetes and Click Create
2. name it, select the region, set the automatic upgrades to disabled, select some small cheapie nodes and then scale manually.
3. Node pools - you can create multiple node pools here or use virtual nodes
4. Access - Azure RBAC or Kubernetes RBAC
5. Networking - if you choose Azure CNI, you'll need to set it inside a VNet. 
- Network Policy as we learned is only selectable
6. Integrations - no ACR integration, no monitoring, etc. 
7. Advanced - leave this
8. Tags - add some basic tags if needed
9. Create the Cluster and wait for it to deploy.

## Tips
---
Note the API address
Note the infrastructure Group - MC_ - the stuff that MS manages

Cluster Configuration - can upgrade your version or set an upgrade policy

## ACR Integration
---
*   Attach AKS to your ACR: `az aks update -n AKSNAME -g AKSRG --attach-acr ACRNAME`
*   Show AKS: `az aks show -g AKSRG -n AKSNAME -o table`
*   (Optional) Upgrade cluster: `az aks upgrade -g AKSRG -n AKSNAME --kubernetes-version VERSION`

# Demo: Deploy an app to AKS using YAML
---
1. Do the previous demo
2. Open VSCode
3. Paste this into a new file:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ausemartweb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ausemartweb
  template:
    metadata:
      labels:
        app: ausemartweb
    spec:
      containers:
      - name: ausemartweb
        image: <IMAGEREF>
        resources:
          limits:
            memory: "128Mi"
            cpu: "100m"
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: ausemartweb
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: ausemartweb
```

4. Save
5. Run `kubectl apply filename.yaml`
6. Look for the public IP on the service LoadBalancer

7. Check the nodes and the workloads on that nodepool to see if your pod is running. 
## Cleanup
---
1. Run `kubectl delete -f filename.yaml`

# AKS Storage Overview
---
Pods are ephemeral - so what happens to the data or what happens if you need to persist data?
You need to define this externally from the 

![image.png](/.attachments/image-bfd65420-75b3-4475-9f27-1d1c44976235.png)

You really want to abstract the storage away from the pod using storage classes and persistent volumes and persistent volume claims
- Storage class - used to define tiers of storage
- Persistent Volume Claim - used to request volume of a specific class from the control plane.

Demo: Configure an Azure Files Volume for an app in AKS
---

1. Check out this YAML file:
```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: sc-azurefile-std
provisioner: file.csi.azure.com
allowVolumeExpansion: true
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=0
  - gid=0
  - mfsymlinks
  - cache=strict
  - actimeo=30
parameters:
  skuName: Standard_LRS
```

Read through it and understand what it does

2. kubectl apply -f file.yaml
3. Create a deployment using this file:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: duposwebappmon
spec:
  replicas: 1
  selector:
    matchLabels:
      app: duposwebappmon
  template:
    metadata:
      labels:
        app: duposwebappmon
    spec:
      containers:
      - name: duposwebapp
        image: <IMAGE>
        resources:
          limits:
            memory: "128Mi"
            cpu: "100m"
        ports:
        - containerPort: 80
      - name: duposwebappmon
        image: curlimages/curl:latest
        command:
          - sh
          - -c
          - watch -n 60 curl -I http://localhost >> /mnt/azure/log.txt
        resources:
          limits:
            memory: "128Mi"
            cpu: "100m"
        volumeMounts:
        - name: volume
          mountPath: "/mnt/azure"
      volumes:
        - name: volume
          persistentVolumeClaim:
            claimName: claim-webapp-azurefile
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: claim-webapp-azurefile
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: sc-azurefile-std
  resources:
    requests:
      storage: 100Gi
--- 
apiVersion: v1
kind: Service
metadata:
  name: duposwebappmon-lb
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: duposwebappmon
```

4. Check in the MC_ Resource Group and you'll see a new Storage Account
![image.png](/.attachments/image-0b9e724f-8e4e-4a2b-af8e-fc5c845d9a3f.png)

## Commands:
---
*   Change to new folder: `cd dev`
*   Setup a new YAML (storage class): `code filename.yaml`
*   Apply YAML: `kubectl apply -f filename.yaml`
*   Setup a new YAML (webmon deployment using SC): `code duposwebmon.yaml`
*   Apply YAML: `kubectl apply -f duposwebmon.yaml`


## Clean Up
---
Delete the deployment
*   Remove deployment: `kubectl delete -f duposwebmon.yaml`


# AKS Autoscale
---
Need to scale the pods AND the nodes

Cluster Autoscaler - increases the number of nodes based on demand
Horizontal Pod Autoscaler - increases the number of replicas

![image.png](/.attachments/image-9b913be6-5801-4569-b272-4004c61b5450.png)

# Demo: Configure Application and Cluster Autoscale
---
1. Look at the same yaml above - change the part in it to say `replicas: 40`
2. Apply that
3. You'll see a warning on the deployments - insufficient mem/cpu, due to the fact we have 1 node and no autoscaling
4. Change the scaling to autoscale and set to 5.
5. Notice that the replicas then start to update to meet the 40.
6. Change the replicas back to 1

![image.png](/.attachments/image-7d802eed-a120-43f8-bf44-c8631aeecf5e.png)

## Horizontal Pod Autoscaling
---
1. Look at this YAML
```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: duposwebmon-hpa
spec:
  maxReplicas: 10 # define max replica count
  minReplicas: 2  # define min replica count
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: duposwebmon
  targetCPUUtilizationPercentage: 20 # target CPU utilization
```
2. Apply this yaml file
3. Create a new pod to generate load
*   Make sure you change <ADDRESS> to match your load balancer
*   Get your load balancer details: `kubectl get service`
    *   `kubectl run load-generator --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.0001; do wget --server-response --spider --quiet http://<LBIPADDRESS> 2>&1 | grep 'HTTP' ; done"`
*   Monitor what's happening
    *   `kubectl get hpa`
    *   `kubectl top pod`
3. Notice that the pods increase up from 1 pod. 

## Clean up
---
Delete the load-generator pod
Delete the deployment
Set it back to manual - 1 node. 

# Azure Container Apps - ACA
---
Container Instances or Kubernetes Services?
Minimal features vs Advanced features
ACA is in the middle - serverless. 

![image.png](/.attachments/image-f1865806-a516-4304-b3bd-323df7fe4ee9.png)

KEDA, DAPR, envoy - Learn these terms :)

Serverless
- Can scale down to zero - does take some time to spin back up.

NOTE: This has no Kubernetes API or control plane access. 

## Prerequisites:
---
- Containers
- Deploy

## Key Components
---
Environment - logging via LA workspace, VNET configured here
Container App - one or more containers that make up your app
Revision - Uses immutable container app snapshots - v1, v2, v3, etc. Can roll back as needed or split between two different versions as a 50/50%

![image.png](/.attachments/image-5bb261c1-01b8-407b-8304-c210d38ad57c.png)

# Demo: Get started with Azure Container Apps
---
Create a Container app
2. Add a RG
3. Name it
4. Select region and create a new Container Apps Environment
5. Create a new LA workspace if needed
6. Create a new VNet if needed
![image.png](/.attachments/image-4f486191-0687-44ba-98cb-c5d0a7c84033.png)
7. Use the ACR that we created earlier, select an image, select CPU and memory, configure environment variables if needed
8. Tag as needed
9. Review and Create
10. Create ingress into this environment. 
- IP restrictions can be set here
11. Access via the URL from the Overview tab. qw

## Revisions
---
1. Edit and deploy
2. Scale with a new scale rule based on HTTP scaling or Azure Queue
3. Scale to like 3 replicas
![image.png](/.attachments/image-3658778b-a3de-46ce-b707-c317e700f97f.png)
4. Split the traffic between the different versions - like deployment slots
![image.png](/.attachments/image-da3a7eac-2ec3-4513-a99e-31b0ddfd7fe5.png)

## Clean Up
---
Delete the Container App and everything associated with it. 

# Case Study - Containerized Solutions
---
Implementing Kubernetes - backend
Unchanged - frontend

Azure CNI would be the networking mode. 
Bursty performance would need to be virtual nodes using container Instances
Premium SKU of ACR for image signing. 























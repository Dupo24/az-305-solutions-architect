[[_TOC_]]
# Virtual Networks
---
What are VNets? - Vnets are private isolated hosting enviromnents. 
![image.png](/.attachments/image-f4d7e9d5-3456-4d5c-97ff-7a3fc764bcd8.png)
Implementation - 
- VNet
- Subnet
- Network interfaces

Virtual network exists in a region and spans all availability zones in a region.
What this looks like: 
![image.png](/.attachments/image-0418703d-1b51-4be8-9103-5b2250d0087b.png)
How to configure:
- need an address space - CIDR notation - /16 on the vnet gives us the ability to give us /24 subnets
- DNS is provided for you inside of the vnet - can select custom DNS such as 8.8.8.8 for Google if you'd like to. 
- protocols, TCP, UDP ICMP TCP/IP
![image.png](/.attachments/image-368b5160-be70-49e3-a14d-dd8ac131e54b.png)

What do we get by default?
- connectivity between subnets - sn1 can talk to sn2 and sn3.
- connectivity out to the Public Internet
- system connectivity - VNet peering - connecting to other VNets. 

![image.png](/.attachments/image-1c883fd3-ab26-4f09-884a-251e770e06d4.png)

# Demo - Create a VNet
---
![image.png](/.attachments/image-45d3d828-8ec3-4679-8299-7d0f61887854.png)
Subnet address range must be within the VNet IP range.
You cannot enable IPv6 on a subnet where IPv6 is not configured on the VNet. 

# IP Addressing
---
- Private IP
- Public IP

![image.png](/.attachments/image-40d24324-1006-45be-9c84-4c7f9a3ea04d.png)

## Private IP addressing
---
- Works by association - 
- IPs are allocated either dynamically or static, but you can't reserve the addresses in advance. You can create the resource, create the interface and then assign the IP to the interface

Considerations:
- cannot allocate the first 4 or the last IP's in a subnet. 

## Public IP
---
Need to create a standalone resource and then associate that resource to your interface.
- basic (deprecating)
- standard

Can be dynamic or static
- if you need a range of IP addresses, assign a `Public IP Prefix` which assigns IP's from a pool
- bring your own IP is also an option. 

## Outbound connectivity
---
- Internet by default
- if no IP is configured, MS will give you a public IP
- public load balancer SNAT - can be routed out via the pubilc IP of a load balancer. 
- NAT Gateway - provides connectivity outbound via private IP conversion to Public IP

## Public services
---
Some services are public by design, such as SQL

# Demo - Create a NAT gateway
---
1. Create a public IP - standard
![image.png](/.attachments/image-27908452-af55-4d44-8a8f-cfaedda53ca4.png)
2. Create a NAT Gateway for a VNet.
![image.png](/.attachments/image-05c6b95a-4f60-42db-96e5-6d3ed45f42ee.png)

# Network Security Groups
---
![image.png](/.attachments/image-f87f60ef-a11c-4244-b055-12c6f543467f.png)
Act like a guard on the "roads" of the network

- list of outbound and inbound traffic allowed or denied. 
- assigned at the subnet or NIC level or both
- each rule defines the type of traffic allowed or denied into the destination of the NSG. 

Set up by priority - lower number is a higher priority. Once the traffic matches a rule, the rest of the rules are dropped. 
There are 3 default rules that cannot be deleted. 

Deny by default - everything is blocked except what you allow.  

Inbound traffic: Subnets take priority over NICs when assigning NSGs. If your NSG on the subnet blocks RDP, creating an NSG and attaching it to a NIC is not going to allow RDP to that machine that the NIC is attached to. 

Outbound traffic: NICs take priority over the subnet NSGs

NSGs attached at the subnet level act as if they are attached to the NICs, so if you deny RDP on the subnet, you will not be able to RDP from one machine in the subnet to another inside of the subnet. 

NSGs are stateful firewalls. If I let you out, I will also let you back in. -NSG guard

# Demo - Create an NSG
---
Microsoft has made it a bit more secure. You need to define inbound RDP and SSH connections by default now. 
1. Create VM
2. Create Public IP on that VM
3. Create NSG with 3389 allowed to the subnet that the VM resides in
4. Connect to VM via public IP. 

# Augmented Security Rules
---
Azure services can be used in rules by using Service Tags. 
Application security groups can also be used. These group VMs together under a common grouping. 

![image.png](/.attachments/image-5f24196f-c4b2-4045-bf5b-28effdca1134.png)

- All VMs in an ASG must be from the same vnet
- All source and destinations must be from the same vnet
- cannot create custom service tags

# Demo - Use ASGs and Service Tags
---
1. Create some VMs
2. Create an ASG
2. Add the VMs to the ASG
4. Create an NSG
5. Add the Service Tags to the Azure Resource Manager and block those from the NSG
6. Create an RDP to the ASG on the NSG
7. Confirm you can RDP to the servers and log into Azure but Azure #fails. 

# Case Study - Networking
---
![image.png](/.attachments/image-f504d110-7caa-4844-9c54-13324c449f85.png)






# Azure Queue Storage
---
A place for messages to be stored before something picks it up to use.
Simpler than Service Bus, not recommended for critical information.

![image.png](/.attachments/image-908068ba-556e-472d-81d0-56911633cbcf.png)

Publisher and Receiver - send and receive messages (XML, JSON, Text, etc) via REST
Storage Account
Queue - endpoint for messages to be published to and recieved - (poll/pull)

![image.png](/.attachments/image-e8a9ef19-9f52-434f-acc2-070d7ef298fa.png)

# Azure Service Bus
---
Enterprise scale messaging service.
Used when you want to guarantee a delivery correctly, not duplicated, not out of order. 
Topics can be used to enhance functionality. 

- FIFO, at most once, at least once guarantees
- supports sessions, dead lettering, duplicate detection and more
- maximum message size of 256kb/100mb, 10,000 queues. 

## Pricing
---
Basic
Standard - shared capacity - max 256kb message, queues and topics
Premium - dedicated - max 1mb message, all of the above plus zone redundancy. 

## Resources
---
Publisher and Receiver - send and receive messages (XML, JSON, Text, etc) via REST
Namespace - container for service bus
Queue - FIFO delivery queue

![image.png](/.attachments/image-6969f24d-a34b-443e-a8f1-23f2f5337a5c.png)

## Topics
---
Endpoint for message publishing
- supports ordering, partitioning, etc

Subscription - messages that are duplicated from a topic can go into these different subscriptions. 

![image.png](/.attachments/image-442354de-b632-4bd6-9b75-f9c1fd559713.png)

# Event Grid
---
This is about events, not messages. Can include IoT devices
- basic service provides lightweight delivery of events

Basic
- publisher subscriber push model

Standard
- IoT, MQTT support, pull model

## Event Grid Topics
---
Event Publisher
Event Handler
Event Grid service
Topics - collection of related published events
![image.png](/.attachments/image-3b790d5d-392d-42e6-9efa-fe3df7a737f8.png)

# Event Hubs
---
Streams of event data
- near realtime
- Supports AMQP, HTTPS, Apache Kafka and more
![image.png](/.attachments/image-d3cfee0b-7838-4252-8ca3-5cd113d516ea.png)
![image.png](/.attachments/image-8bed35d9-15d6-48a1-b229-61bde9255054.png)

## Components
---
Event Hub Namespace
Event Hub
Partition
Consumer group - a view of the hub to see where your events are. 

![image.png](/.attachments/image-1181bded-e573-4233-af1b-cb44f1b55cca.png)

# Azure API Management
---
- API documentation
- Access to the APIs via API Gateway
![image.png](/.attachments/image-4d391deb-2695-409a-b1f6-44b6297cd8c2.png)

Basic v2 - dev test
Standard v2 - production, development portal

Management plane 
Rate limits and quotas, security validation. caching, transformations and self hosted options. 

No more v1 :(

![image.png](/.attachments/image-2e9d3f2d-7ab8-4e3a-aa0c-d7ac6b19b1a0.png)

# Azure Logic Apps
---
Trigger - time based
Does something
GUI based workflows with connectors for various services

## Components
---
Logic App Resource
Workflow (can save as JSON)
Triggers and Actions
Connectors

## Pricing Models
---
Consumption
Standard
![image.png](/.attachments/image-5e99a0d9-0636-4ff5-bf0b-184ce5a55c52.png)

# Case Study
---
https://learn.cantrill.io/courses/az-305-microsoft-azure-solutions-architect/lectures/48733866

- All APIs are exposed to the Internet
- no caching on the APIs
- slower responses to negative reviews
- handled on manual basis


Solution:
- Turn off backend public access using APIM Standard v2
- Logic App for feedback to create a SN ticket

![image.png](/.attachments/image-738c7ecc-12be-4baa-8d13-1005a1328608.png)



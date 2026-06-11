- Waterfall Model
- Agile Model
- Devops: Continuous Intergration and Development
- Devops Lifecycle
  - Plan --> Code --> Build --> Test --> Continuous Integration --> Continusous Deployment --> Continuos Monitoring

---

Date:13-04-2026

## Client Server Architecture

- What is client?
  - Client is the requestee who makes request for a resource locally or online
  - Which request a resource
  - Always requesting
- What is server?
  - Which respond to the request
- How the communicate with each other?
  - Using Network
  - Always responding

- What is Network?
  - Components:Device
  - If device requesting: Client
  - If responding to request:Server
- Types of Client-Server Architecture:
  1.  1-Tier
  2.  2-Tier
  3.  3-Tier

- 1 Tier Architecture
  - client and server are locally located inside a local device
  - client and device in same laptop
  - client and server in same machine
- 2 Tier Architecture
  - Two separate machine for client and server
  - Overhead:Network(to connect client and server)a
  - Server(complete Persistency and Logic Layer)
  - Hardware constraints hard to scale Servers
  - Performance degrades as request increases
  - Security Concerns
- What is Production Environment?
  - Customers are accessing application deployed on server
  - The server environment is Production Environment
- 3 Tier Architecture:
  - Separe client,application,and data layer
  - Easy scale
  - more secure
  - Overhead:Networking and middleware
- Every Server: IP Address,and Hostname
- What is IP?
  - How it works IP
  - How IP is provided to machine
  - HOw every machine has unique IP
- WebServer?
  - Why it is needed: To handle request and redirect to application server

---

Date: 15/4/2026

- Network Flow of a SaaS:

- DNS(Domain Name Server):
  - What is DNS?
  - What is it's main function
  - What happens without DNS
  - It keep track of all hostname and IP address
  - How it works complete mechanics
  - What are it's vulnerabilities
  - What are it's overheads
  - What are it's constraint

  - What are layers of DNS:
    - Local DNS
    - Root name server
    - top-level-domain
    - Name Server:Identify the domain name
    - SOA:get the IP Address of the domain

  - Firewall:
    - What is function of firewall
    - What happens without firewall
    - Vulnerabilites and constraints of Firewall
  - Network Protocol
    - Application Layer
      - http: Non secure
        - port:80
      - https: Secure
        - port:443
      - What makes https secure
      - ssh
        - port:22
      - rdp
        - port:3389

  - Load Balancer
    - What are it's functionality
    - What happens without it
    - How it handles load explain it's mechanics
  - Web-Server
  - App Server
  - Database server

  - Commands:
    - nslookup

---

Date:17/4/2026

- HTTP(Hypertext Transfer Protocol)
	- Default Port No.:80
	- What is a Port
	- How it works
- HTTPS(Hypertext Transfer Protocol Secure)
	- Default Port No.:443
- How loadbalancer handles ports:
	- like port conversions
- How HTTP Transfers data from client to server and server to client:
	- Complete mechanics
- Request & Response Status Codes:
	- 404: Page not found
	- 500: Internal server error
	- 503: Service Unvailable
	- 200: Page found/Success
- Why HTTPS is secure ?
	- What is the security vulnerability of http
	- How https solves that vulnerability
	- What is  certificate and how it works?
		- What is a SSl/TLS certificate
- What is a datapacket
	- what info it carries
- What is TCP?
	- How it works
	- How it enables https
	- complete mechanics
- What is UDP?
	- What is the problem with UDP
	- What makes less reliable comapare to TCP
- when to use which protocol
- What is OSI Layer  
---
- Pre-cloud 
	- Overhead of infrastructure
	- More initial cost
	- Hard to scale
	- Maintenance Cost
	- Less Flexibility:Related OS and hardware
	- More Security and Privacy
	- Less dependency on Network
	- Very Expensive
- Virtualisation:
	- What is virutalisation
	- How virtualisation works complete mechanics and how each layer and software,hardware help us to virtualise
	- What are the benefits of Virtualisation
	- What are the constraints of virtualisation
	- What are the overheads and cost of virtualisation
	- What are the benefits of virtualisation
- P2V Migration:
	- How it works
	- How to do it 
	- Precautions
	- Complete workflow
- V2C Migration
	  - How it works
	  - How to do it
	  - Precautions
	  - Complete Workflow

- Cloud Computing
	- What is cloud?
	- What is it's causality
	- What problem it solves and how it solves it
	- What happens without cloud
	- What technology are necessary for cloud and are backbone of it
		- How each this technology works
		- Provide an analogy
- What is meant by IaaS
- AWS data-centers:33
- What is AwS
- What is Computing?
	- Computing is the method of using electronic devices to perform tasks
	- Cloud Computing: Computing using remote servers over the network
- Deployment Models in Cloud:Public Cloud,Private Cloud,Hybrid Cloud
- What is Public Cloud?:Provider services which are accessed by everyone
- What is Private Cloud?:Provider services which are accessed within the organisation
- What is Hybrid Cloud?: Combination Public and Hybrid Cloud

- What are Service Models?
	- IaaS:Infrastructure as a Service
	- PaaS:Platform as a Service
	- SaaS:Software as a Service

---
Date:20/4/2026
- Amazon Computing Services:
	- EC2(Elastic Compute Cloud)
		- It enables us to create/launch VM's on remote server
		- While launching we need to select the specificatoions of EC2:
			- Firewall configuration
			- OS Images:Linux,Ubuntu,Red-Hat
			- Hardware Specifications:Cores,RAM,storage
			- Explain what features it provide
        		- How it works
        		- Use cases
        		- What problems it solves
- IaaS:Client Responsibility: App,Data,OS | Provider Responsibility:Infrastructure,Access Console,Various configurable feature to configure the Infrastructure according to client needs

- PaaS:
	- Client Responsibility: Application,Data
	- Provider Responsibility:OS,Network,Infra,Configurations
- SaaS:
	- Client Repsonsibility: Only using the software
	- Provider Responsibility: Everything

- EBS(Elastic Beans Stalk):PaaS service used for fast deployment
	- Explain what features it provide
	- How it works 
	- Use cases
	- What problems it solves
	- What we need to configure

---

Date:23/04/2026
- 3T's
	- Elasticity
	- Scalability
	- High Availability

- What is Elasticity:
	-   Increasing or decreasing the no. instances based on Load is called Elasticity
	- How it is achieved:
		- Principle and Technology behind
		- Explain complete mechanics with eg.
	- What is autoscaling
		- Automated scale out and scale in
		- How it happen automatically
	- Where Elasticity is feasible and where not
	- What are the constraints of Elasticity
	- What are the advantages of Elasticity
	- What is the cost vs benefit of Elasticity
	- Precautions while performing Elasticity
	- Is elasticity same as Horizontal Scaling or different
	- Duration: Short term
	- How is it measured and monitor
	- What are it's KPIs

- What is Scalability
	- Scalability: Increasing the capacity of the server
	- What Principle and technology is used to achieve scalability
		- Explain complete mechanics with eg.
	- Is scalability to vertical scaling
	- Duration:Long term
	- Scalability is achieved: Changing Instance configuration
	- Where Scalability is feasible and where not
	- What are the constraints of scalability
	- What are the advantages of scalability
	- What is the cost vs benefit of Scalability
	- Precautions while Performing Scalability
	- How is it measured and monitor
	- What are the KPIs

- High Availability:
	a- Any Service should be available all time
	- How high-availability is achieved
	- What principle and technology is used to achieve high-availability
		- Explain complete mechanics with eg.
	- What breaks high-availability
	- Where High-availability is feasible and when not
	- What are the constraints of high availability
	- What are the advantages of high avaialability
	- What is the cost vs benefit of High-Availability
	- Precautions while achieving high Availability
	- How it is measured
	- What are the KPIs
- What is Redundancy in Servers?
- How we check a server is down?
	- Explain the mechanics
	- Explain the causes of server down
	- And how to trouble shoot this problem
- What is the concept Failover
	- How it helps high availability
	- Explain the mechanism in detail
- Why High-Availability: 
	- Depends: on autoscaling:
		- How autoscaling is a fault tolerance mechanism
- What is availability metrics and how to calculate down-time

---

- Availability Zones and Region
- What is a Availability zone and Region?
	- Region: Geographical Area where AWS has it's Infrastructure	
	- Availability Zone:
	- How Availability Zone is important 
		- What role it plays in system design and configuration
		- How to choose availability zone or Region
		- What things to take into consideration while deciding availability zone of a cloud service
		- What factor one should consider while deciding availability zone and how to reason the decisions
	- Region Code:ap-south-1
	- Availability Zones code: ap-south-1a,ap-south-1b,ap-south-1c
- What should be Region selection strategy to maintain High Availability always?
- AZ's are sync with each other network not data?
- What is meant by Latency?
	- What metric it measures
	- What is the desired value for it
	- How to achieve low latency in request response cycle while deciding availability zones
	
- Can two regions communicate with each other and if yes how?
- EC2 is bounded by Region and Availability Zone
- LB: How load balancer works in AWS?
	- Is it specific to region or Availability zone
	- How to architecht a High Availability System in AWS explain the architecture and how it takes care of elasticity,scalability,Redundancy,Failover,Faul-tolerance

- What is VPC? 
	- VPC:Virtual Private Cloud
	- What is causality for VPC
	- What breaks without VPC
	- How VPC is important while architecting cloud systems:
		- Explain the break points without VPC with simple analogy
	- How VPC handles security
	- What is default VPC provided by AWS and how it is different from our own VPC.

--- 
Date: 24/4/2026

## EC2 Service
- EC2:Elastic Compute Clound
- Service to launch VM instances
- EC2 is a Regional service
- What is meant by Regional Services what are the constraints
- What to launch instances using instance and manage them using EC2
- How to configure EC2 instance what things to take care while configuring launching and using EC2 instances
- How to decide the configuration 
	- What factors and system design to consider while selecting the images network configuration and hardware configuration while creating and launching instances

## ELB Service:
- ELB: Elastic Load Balancer
- What is ELB
- The Role of ELB
- is ELB a regional service or global
- Use cases of ELB
- What architectural decisions to consider while using ELB
- When to use ELB and when not
- How to configure and use ELB service

## LighSail:
- What is LightSail
- How it works 
- When to use Light sail and when not to
- Constraints and overhead of lightsail and the reasoning for each constraint
- Advantages of Lightsail
- Explain complete internal mechanics of lightsail
- How to configure and use LightSail service

## Elastic BeanStalk
- What is Elastic Bean Stalk
- How is different from EC2
- When to use BeanStalk 
- When not to use BeanStalk
- Constraints of Beanstalk
- Advantages of Beanstalk
- Explain complete internal mechanics of Beanstalk
- How to use,manage BeanStalk Service
- What architectural system decision to consider when using Beanstalk

## VPC
- What is VPC
- When to use VPC
- When not to use VPC
- Constraints of VPC
- Advantages of VPC
- Explain complete internal mechanics of VPC
- How to use,manage VPC Service
- What architectural system decision to consider when using VPC

## EventBridge
- What is EventBridge
- When to use EventBridge
- When not to use EventBridge
- Constraints of EventBridge
- Advantages of EventBridge
- Explain complete internal mechanics of EventBridge
- How to use,manage EventBridge Service
- What architectural system decision to consider when using EventBridge

## Lambda
- What is Lambda
- When to use Lambda
- When not to use Lambda
- Constraints of Lambda
- Advantages of Lambda
- Explain complete internal mechanics of Lambda
- How to use,manage Lambda Service
- What architectural system decision to consider when using Lambda
- Why Lambda is called Serverless though internally it must be using a server
---
Date:26/4/2026
## S3
- What is S3
- When to use S3
- Various components of S3: bucket,object,key
- When not to use S3
- Constraints of S3
- Advantages of S3
- Explain complete internal mechanics of S3
- How to use,manage S3 Service
- What architectural system decision to consider when using S3
- S3=Simple Storage Service

## SNS:(simple Notification Service)
## SES:(simple email Service)

## EBS(Elastic Block Storage)
- What is EBS
- What is EBS Volume
- When to use EBS
- When not to use EBS
- Constraints of EBS
- Advantages of EBS
- Explain complete internal mechanics of EBS
- How to use,manage EBS Service
- What architectural system decision to consider when using EBS
- How EBS is Different from S3
- What is difference between root volume and EBS volume in EC2
- How volume size can be increase on Fly without downtime
- What is Device name and root volum device name:
	- What is the purpose of Device name 
	- root volume: /dev/sda1
- Volumes and EC2 must be inside same Availability Zone

## EFS(Elastic File System)
- What is EFS
- When to use EFS
- Various components of EFS: 
- When not to use EFS
- Constraints of EFS
- Advantages of EFS
- Explain complete internal mechanics of EFS
- How to use,manage EFS Service
- What architectural system decision to consider when using EFS
- What is NFS protocol and how it used in EFS
- what is concept of replication in EFS
- Basic deploy architecture and scenarios for EFS
---
Date:27/4/2026
## SNOW Family:
- What is SNOW Family
- When to use SNOW Family
- Various components of SNOW Family:
- When not to use SNOW Family
- Constraints of SNOW Family
- Advantages of SNOW Family
- Explain complete internal mechanics of SNOW Family
- How to use,manage SNOW Family Service
- What architectural system decision to consider when using SNOW Family
- Basic deploy architecture and scenarios for SNOW Family

## Glacier:
- What is Glacier
- When to use Glacier
- Various components of Glacier:
- When not to use Glacier
- Constraints of Glacier
- Advantages of Glacier
- Explain complete internal mechanics of Glacier
- How to use,manage Glacier Service
- What architectural system decision to consider when using Glacier
- Basic deploy architecture and scenarios for Glacier

## Storage Gateway:
- Help us to mount amazon storage service to our on-premise devices
- What is Storage Gateway
- When to use Storage Gateway
- Various components of Storage Gateway:
- When not to use Storage Gateway
- Constraints of Storage Gateway
- Advantages of Storage Gateway
- Explain complete internal mechanics of Storage Gateway
- How to use,manage Storage Gateway Service
- What architectural system decision to consider when using Storage Gateway
- Basic deploy architecture and scenarios for Storage Gateway

## RDS(Relational Database Service)
- It is PaaS
- What is RDS
- When to use RDS
- Various components of RDS:
- When not to use RDS
- Constraints of RDS
- Advantages of RDS
- Explain complete internal mechanics of RDS
- How to use,manage RDS Service
- What architectural system decision to consider when using RDS
- Basic deploy architecture and scenarios for RDS
- RDS supports:7 Engines:MOMPMAI:MySQL,Oracle,MariaDB,PostgreSQL,MSSQL,Aurora,IBM DB2

## DMS(Database Migration Service):
- What is DMS
- When to use DMS
- Various components of DMS:
- When not to use DMS
- Constraints of DMS
- Advantages of DMS
- Explain complete internal mechanics of DMS
- How to use,manage DMS Service
- What architectural system decision to consider when using DMS
- Basic deploy architecture and scenarios for DMS

## DynamoDB(NoSQL)
- What is DynamoDB
- When to use DynamoDB
- Various components of DynamoDB:
- When not to use DynamoDB
- Constraints of DynamoDB
- Advantages of DynamoDB
- Explain complete internal mechanics of DynamoDB
- How to use,manage DynamoDB Service
- What architectural system decision to consider when using DynamoDB
- Basic deploy architecture and scenarios for DynamoDB

## Redshift(DataWarehouse)
- What is Redshift
- When to use Redshift
- Various components of Redshift:
- When not to use Redshift
- Constraints of Redshift
- Advantages of Redshift
- Explain complete internal mechanics of Redshift
- How to use,manage Redshift Service
- What architectural system decision to consider when using Redshift
- Basic deploy architecture and scenarios for Redshift

## ElasticCache
- In memory database caching service
- Two Engines: Redis,MemCached
- What is ElasticCache
- When to use ElasticCache
- Various components of ElasticCache:
- When not to use ElasticCache
- Constraints of ElasticCache
- Advantages of ElasticCache
- Explain complete internal mechanics of ElasticCache
- How to use,manage ElasticCache Service
- What architectural system decision to consider when using ElasticCache
- Basic deploy architecture and scenarios for ElasticCache

---
Date:28/4/2026

## Route53
- DNS service in AWS
- DNS port no:53
- What is Route53
- When to use Route53
- Various components of Route53:
- When not to use Route53
- Constraints of Route53
- Advantages of Route53
- Explain complete internal mechanics of Route53
- How to use,manage Route53 Service
- What architectural system decision to consider when using Route53
- Basic deploy architecture and scenarios for Route53
- It is a Global Service

## VPN
- What is VPN
- When to use VPN
- Various components of VPN:
- When not to use VPN
- Constraints of VPN
- Advantages of VPN
- Explain complete internal mechanics of VPN
- How to use,manage VPN Service
- What architectural system decision to consider when using VPN
- Basic deploy architecture and scenarios for VPN
- It is a Global Service

## Direct Connect
- What is Direct Connect
- When to use Direct Connect
- Various components of Direct Connect:
- When not to use Direct Connect
- Constraints of Direct Connect
- Advantages of Direct Connect
- Explain complete internal mechanics of Direct Connect
- How to use,manage Direct Connect Service
- What architectural system decision to consider when using Direct Connect
- Basic deploy architecture and scenarios for Direct Connect
- It is a Global Service

## CloudFront
- What is CloudFront
- When to use CloudFront
- Various components of CloudFront:
- When not to use CloudFront
- Constraints of CloudFront
- Advantages of CloudFront
- Explain complete internal mechanics of CloudFront
- How to use,manage CloudFront Service
- What architectural system decision to consider when using CloudFront
- Basic deploy architecture and scenarios for CloudFront
- What is edgelocation
	- how it works
	- it's use
	- constraints of it 
	- advantages of it
- How CloudFront help us to achieve low latency accross different regions
- How the cache mechanism works
- What is the concept of TTL(Time to live):
	- How it works
	- constraints of it
	- advantages of it
- What is concept of Invalidate cache
- What is CDN and how it works?
	- It's use in Cloud Front

---

Date: 29/4/2026

## IAM(Identity and Access Management)
- What is Root User:
- User account
- What is IAM User 
- Difference between IAM User and Root User
- What is IAM
- When to use IAM
- Various components of IAM:
- When not to use IAM
- Constraints of IAM
- Advantages of IAM
- Explain complete internal mechanics of IAM
- How to use,manage IAM Service
- What architectural system decision to consider when using IAM

## SQS
- What is SQS
- When to use SQS
- Various components of SQS:
- When not to use SQS
- Constraints of SQS
- Advantages of SQS
- Explain complete internal mechanics of SQS
- How to use,manage SQS Service
- What architectural system decision to consider when using SQS

## AWS Inspector
- What is AWS Inspector
- When to use AWS Inspector
- Various components of AWS Inspector:
- When not to use AWS Inspector
- Constraints of AWS Inspector
- Advantages of AWS Inspector
- Explain complete internal mechanics of AWS Inspector
- How to use,manage AWS Inspector Service
- What architectural system decision to consider when using AWS Inspector

## AWS Trusted Advisor

- What is Trusted Advisor
- When to use Trusted Advisor
- Various components of Trusted Advisor:
- When not to use Trusted Advisor
- Constraints of Trusted Advisor
- Advantages of Trusted Advisor
- Explain complete internal mechanics of Trusted Advisor
- How to use,manage Trusted Advisor Service
- What architectural system decision to consider when using Trusted Advisor

## AWS Organisations
- What is an organisation
- What is the concept of OU's
- How inside organisation we can also control root users which are part of organisation
- Who user manages an organisation
- Explain complete Organisation Architecture using a real Company analogy and explain each aspect of this service when used in real world
- What are the components of Organisation
- What are SCPs and RCPs
- How to architect and use this service
- Constraints 
- Use cases

- What is Amazon Account ID 


## CloudWatch
- What is CloudWatch
- When to use CloudWatch
- Various components of CloudWatch:
- When not to use CloudWatch
- Constraints of CloudWatch
- Advantages of CloudWatch
- Explain complete internal mechanics of CloudWatch
- How to use,manage CloudWatch Service
- What architectural system decision to consider when using CloudWatch
- What is an Alarm
- How to set and configure alarms
- What is difference between Basic Monitoring and Detailed Monitoring

## CloudTrail
- What is CloudTrail
- When to use CloudTrail
- Various components of CloudTrail:
- When not to use CloudTrail
- Constraints of CloudTrail
- Advantages of CloudTrail
- Explain complete internal mechanics of CloudTrail
- How to use,manage CloudTrail Service
- What architectural system decision to consider when using CloudTrail

## Config
- What is AWS config
- When to use AWS config
- Various components of AWS config:
- When not to use AWS config
- Constraints of AWS config
- Advantages of AWS config
- Explain complete internal mechanics of AWS config
- How to use,manage AWS config Service
- What architectural system decision to consider when using AWS config

- How AWS cloudwatch,cloudtrail,config works as provide a realworld example and explain their working step by step in this example

## Certificate Manager
- What are certificates
- How to use them
- Explain the mechanics of certificates in detail
- What is Certificate Manager
- When to use Certificate Manager
- Various components of Certificate Manager:
- When not to use Certificate Manager
- Constraints of Certificate Manager
- Advantages of Certificate Manager
- Explain complete internal mechanics of Certificate Manager
- How to use,manage Certificate Manager Service
- What architectural system decision to consider when using Certificate Manager

## Keys Manager
- What are keys
- How they encrypt data
- How ,when and where to use them
- What is Key manager
- When to use Key manager
- Various components of Key manager:
- When not to use Key manager
- Constraints of Key manager
- Advantages of Key manager
- Explain complete internal mechanics of Key manager
- How to use,manage Key manager Service
- What architectural system decision to consider when using Key manager

## AWS Secrets
- What are secrets
- How to use them
- What is Secrets
- When to use Secrets
- Various components of Secrets:
- When not to use Secrets
- Constraints of Secrets
- Advantages of Secrets
- Explain complete internal mechanics of Secrets
- How to use,manage Secrets Service
- What architectural system decision to consider when using Secrets

## AWS Backup
- What is AWS Backup
- When to use AWS Backup
- Various components of AWS Backup:
- When not to use AWS Backup
- Constraints of AWS Backup
- Advantages of AWS Backup
- Explain complete internal mechanics of AWS Backup
- How to use,manage AWS Backup Service
- What architectural system decision to consider when using AWS Backup

## AWS Shield
- What are DDoS attacks
- explain the mechanics of DDoS attack and how to defend against them 
- How the defence mechanism works
- What is AWS Shield
- When to use AWS Shield
- Various components of AWS Shield:
- When not to use AWS Shield
- Constraints of AWS Shield
- Advantages of AWS Shield
- Explain complete internal mechanics of AWS Shield
- How to use,manage AWS Shield Service
- What architectural system decision to consider when using AWS Shield

## WAF
- What is WAF
- When to use WAF
- Various components of WAF:
- When not to use WAF
- Constraints of WAF
- Advantages of WAF
- Explain complete internal mechanics of WAF
- How to use,manage WAF Service
- What architectural system decision to consider when using WAF

## AWS Support
- Explain various types of support provided by AWS

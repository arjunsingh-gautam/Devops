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

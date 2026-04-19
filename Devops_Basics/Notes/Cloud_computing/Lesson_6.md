
# <span style="color:#a7c957"><strong>Cloud Deployment Models — Public Cloud, Private Cloud, Hybrid Cloud</strong></span>

Cloud deployment models describe **how cloud infrastructure is owned, accessed, and managed**.

They define **who controls the infrastructure and who can access it**.

The three primary deployment models are:

```text
Public Cloud
Private Cloud
Hybrid Cloud
```

Each model provides **different trade-offs between cost, control, security, and scalability**.

---

## 🔗 Navigation (H2 Anchors)

* [#overview](#overview) — **Overview of Cloud Deployment Models**
* [#public-cloud](#public-cloud) — **Public Cloud**
* [#public-mechanics](#public-mechanics) — **How Public Cloud Works**
* [#private-cloud](#private-cloud) — **Private Cloud**
* [#private-mechanics](#private-mechanics) — **How Private Cloud Works**
* [#hybrid-cloud](#hybrid-cloud) — **Hybrid Cloud**
* [#hybrid-mechanics](#hybrid-mechanics) — **How Hybrid Cloud Works**
* [#comparison](#comparison) — **Comparison of Deployment Models**
* [#when-to-use](#when-to-use) — **When to Use Each Model**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="overview"></a> <span style="color:#6a994e"><strong>Overview of Cloud Deployment Models</strong></span>

Cloud deployment models define **how cloud infrastructure is structured and accessed**.

Basic architecture types:

```text
Public Cloud
   │
Private Cloud
   │
Hybrid Cloud
```

Each model differs in **ownership, accessibility, and security**.

---

# <a id="public-cloud"></a> <span style="color:#6a994e"><strong>Public Cloud</strong></span>

Public cloud is a model where **cloud infrastructure is owned and operated by a third-party provider and shared among multiple customers**.

Definition:

```text
Public Cloud = Provider services accessed by anyone over the internet
```

Examples of public cloud providers:

* Amazon Web Services (AWS)
* Microsoft Azure
* Google Cloud Platform

Example infrastructure:

```text
Cloud Provider Data Center
   │
Shared Infrastructure
   │
Multiple Customers
```

Users rent resources such as:

```text
Virtual machines
Storage
Databases
Networking
```

Access is provided through:

```text
Internet
APIs
Cloud consoles
```

---

# <a id="public-mechanics"></a> <span style="color:#6a994e"><strong>How Public Cloud Works</strong></span>

Public cloud providers build **large global data centers**.

Infrastructure structure:

```text
Cloud Data Center
   ├── Physical Servers
   ├── Virtualization Layer
   ├── Cloud Management Platform
   └── Customer Resources
```

Process:

1. User requests resources
2. Cloud platform allocates virtual infrastructure
3. Applications run on shared hardware

Example workflow:

```text
User Request
   │
Cloud API
   │
Virtual Machine Provisioned
   │
User Application Runs
```

---

# <a id="private-cloud"></a> <span style="color:#6a994e"><strong>Private Cloud</strong></span>

Private cloud is a model where **cloud infrastructure is dedicated to a single organization**.

Definition:

```text
Private Cloud = Cloud infrastructure accessible only within an organization
```

Infrastructure may be hosted:

* inside company data centers
* in dedicated cloud infrastructure

Example architecture:

```text
Organization Data Center
   │
Private Cloud Platform
   │
Internal Applications
```

Examples of private cloud technologies:

* OpenStack
* VMware vSphere
* Microsoft Azure Stack

Access is limited to:

```text
Internal networks
VPN access
```

---

# <a id="private-mechanics"></a> <span style="color:#6a994e"><strong>How Private Cloud Works</strong></span>

Private cloud environments use virtualization and automation to create **internal cloud platforms**.

Example architecture:

```text
Organization Data Center
   │
Virtualization Layer
   │
Cloud Management Platform
   │
Internal Services
```

Features include:

* self-service infrastructure
* internal virtual machines
* automated resource allocation

Users inside the organization can provision resources similarly to public cloud.

---

# <a id="hybrid-cloud"></a> <span style="color:#6a994e"><strong>Hybrid Cloud</strong></span>

Hybrid cloud combines **private cloud infrastructure with public cloud services**.

Definition:

```text
Hybrid Cloud = Combination of private cloud and public cloud infrastructure
```

Example architecture:

```text
Private Cloud
     │
     │ Secure Connection
     │
Public Cloud
```

Applications can run across both environments.

Example scenario:

```text
Sensitive workloads → Private cloud
Scalable workloads → Public cloud
```

---

# <a id="hybrid-mechanics"></a> <span style="color:#6a994e"><strong>How Hybrid Cloud Works</strong></span>

Hybrid cloud connects on-premise infrastructure with public cloud environments.

Connection technologies include:

* VPN tunnels
* dedicated network links
* secure APIs

Example architecture:

```text
Company Data Center
       │
Secure Network Connection
       │
Public Cloud Provider
```

Workload distribution example:

```text
Internal database → Private cloud
Web application → Public cloud
```

This allows **flexible workload placement**.

---

# <a id="comparison"></a> <span style="color:#6a994e"><strong>Comparison of Deployment Models</strong></span>

| Feature                | Public Cloud   | Private Cloud | Hybrid Cloud |
| ---------------------- | -------------- | ------------- | ------------ |
| Ownership              | Cloud provider | Organization  | Both         |
| Infrastructure sharing | Shared         | Dedicated     | Mixed        |
| Scalability            | Very high      | Limited       | High         |
| Security control       | Lower          | High          | Balanced     |
| Cost                   | Lower upfront  | Higher        | Variable     |

Each model balances **cost, scalability, and control differently**.

---

# <a id="when-to-use"></a> <span style="color:#6a994e"><strong>When to Use Each Model</strong></span>

### Public Cloud

Best for:

```text
Startups
Web applications
Scalable SaaS platforms
```

Advantages:

* low cost
* rapid scaling
* minimal infrastructure management

---

### Private Cloud

Best for:

```text
Financial institutions
Government systems
Highly regulated industries
```

Advantages:

* full control
* higher security
* compliance support

---

### Hybrid Cloud

Best for:

```text
Large enterprises
Organizations with legacy infrastructure
Gradual cloud migration
```

Advantages:

* flexibility
* workload optimization
* secure data management

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of cloud deployment models like **housing options**.

| Cloud Model   | Real-World Analogy                                                   |
| ------------- | -------------------------------------------------------------------- |
| Public Cloud  | Renting an apartment in a large building                             |
| Private Cloud | Owning a private house                                               |
| Hybrid Cloud  | Living in a private house while renting extra apartments when needed |

Example usage:

```text
Apartment building → Shared infrastructure
Private house → Dedicated infrastructure
Combination → Hybrid setup
```

Key idea:

> **Cloud deployment models determine who owns the infrastructure, who can access it, and how workloads are distributed across computing environments.**

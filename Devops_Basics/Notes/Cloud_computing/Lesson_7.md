
# <span style="color:#a7c957"><strong>Cloud Service Models — IaaS, PaaS, SaaS</strong></span>

Cloud **service models** describe **how much infrastructure the cloud provider manages vs how much the user manages**.

They define **which layers of computing are provided as a service**.

The three main service models are:

```text
IaaS → Infrastructure as a Service
PaaS → Platform as a Service
SaaS → Software as a Service
```

Think of them as **different levels of abstraction in cloud computing**.

---

## 🔗 Navigation (H2 Anchors)

* [#overview](#overview) — **Overview of Cloud Service Models**
* [#layers](#layers) — **Computing Stack Layers**
* [#iaas](#iaas) — **Infrastructure as a Service**
* [#iaas-mechanics](#iaas-mechanics) — **How IaaS Works**
* [#paas](#paas) — **Platform as a Service**
* [#paas-mechanics](#paas-mechanics) — **How PaaS Works**
* [#saas](#saas) — **Software as a Service**
* [#saas-mechanics](#saas-mechanics) — **How SaaS Works**
* [#comparison](#comparison) — **Comparison of Service Models**
* [#analogy](#analogy) — **Real-World Analogies**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="overview"></a> <span style="color:#6a994e"><strong>Overview of Cloud Service Models</strong></span>

Cloud services are layered.

Each model provides **a different level of managed infrastructure**.

```text
User Control
│
│  IaaS  → Most control
│  PaaS
│  SaaS  → Least control
│
Provider Responsibility
```

Higher-level services reduce **operational complexity**.

---

# <a id="layers"></a> <span style="color:#6a994e"><strong>Computing Stack Layers</strong></span>

Cloud services operate on the **computing stack**.

```text
Applications
Runtime
Middleware
Operating System
Virtualization
Servers
Storage
Networking
```

Responsibility distribution:

| Layer          | IaaS     | PaaS     | SaaS     |
| -------------- | -------- | -------- | -------- |
| Applications   | User     | User     | Provider |
| Runtime        | User     | Provider | Provider |
| Middleware     | User     | Provider | Provider |
| OS             | User     | Provider | Provider |
| Virtualization | Provider | Provider | Provider |
| Servers        | Provider | Provider | Provider |
| Storage        | Provider | Provider | Provider |
| Networking     | Provider | Provider | Provider |

---

# <a id="iaas"></a> <span style="color:#6a994e"><strong>IaaS (Infrastructure as a Service)</strong></span>

IaaS provides **basic computing infrastructure**.

Definition:

```text
IaaS = Cloud provider offers virtualized hardware resources.
```

Resources provided include:

* virtual machines
* storage
* networking
* load balancers

Examples:

* AWS EC2
* Azure Virtual Machines
* Google Compute Engine

Example architecture:

```text
User Application
      │
Operating System
      │
Virtual Machine
      │
Cloud Infrastructure
```

Users manage most software layers.

---

# <a id="iaas-mechanics"></a> <span style="color:#6a994e"><strong>How IaaS Works</strong></span>

Example workflow:

### Step 1 — User requests infrastructure

```text
Create VM
```

---

### Step 2 — Cloud platform allocates virtual resources

Example allocation:

```text
CPU
RAM
Disk
Network
```

---

### Step 3 — User installs operating system

Example:

```text
Ubuntu
Windows Server
```

---

### Step 4 — User deploys application

Example:

```text
Web server
Database
Backend services
```

IaaS gives **maximum flexibility**.

---

# <a id="paas"></a> <span style="color:#6a994e"><strong>PaaS (Platform as a Service)</strong></span>

PaaS provides **a complete development platform for building applications**.

Definition:

```text
PaaS = Cloud provider manages infrastructure and runtime environment.
```

Developers focus on **application code**.

Examples:

* Google App Engine
* Heroku
* AWS Elastic Beanstalk
* Azure App Service

Architecture:

```text
Application Code
      │
Platform Runtime
      │
Cloud Infrastructure
```

Users do not manage:

* operating system
* runtime environment
* infrastructure

---

# <a id="paas-mechanics"></a> <span style="color:#6a994e"><strong>How PaaS Works</strong></span>

Typical PaaS workflow:

---

### Step 1 — Developer writes application

Example languages:

```text
Python
Node.js
Java
```

---

### Step 2 — Upload code to platform

Example:

```text
git push
```

---

### Step 3 — Platform automatically provisions infrastructure

Platform sets up:

```text
servers
runtime environment
scaling
network configuration
```

---

### Step 4 — Application runs automatically

Developers focus on **code instead of infrastructure**.

---

# <a id="saas"></a> <span style="color:#6a994e"><strong>SaaS (Software as a Service)</strong></span>

SaaS provides **complete software applications over the internet**.

Definition:

```text
SaaS = Fully managed software delivered via the cloud.
```

Users simply access the application.

Examples:

* Google Workspace
* Salesforce
* Slack
* Dropbox

Architecture:

```text
User
  │
Internet
  │
Cloud Application
```

Users do not manage any infrastructure.

---

# <a id="saas-mechanics"></a> <span style="color:#6a994e"><strong>How SaaS Works</strong></span>

Typical SaaS workflow:

---

### Step 1 — User accesses application

Example:

```text
Open browser
Visit application website
```

---

### Step 2 — User authenticates

Example:

```text
Login credentials
```

---

### Step 3 — Application runs on cloud infrastructure

Cloud provider manages:

```text
servers
databases
scaling
security
updates
```

---

### Step 4 — User interacts with application

Example:

```text
Send emails
Manage documents
Track sales
```

Users focus only on **using the software**.

---

# <a id="comparison"></a> <span style="color:#6a994e"><strong>Comparison of Service Models</strong></span>

| Feature                   | IaaS | PaaS     | SaaS     |
| ------------------------- | ---- | -------- | -------- |
| Control                   | High | Medium   | Low      |
| Infrastructure management | User | Provider | Provider |
| Application management    | User | User     | Provider |
| Complexity                | High | Medium   | Low      |

Each model trades **control for convenience**.

---

# <a id="analogy"></a> <span style="color:#6a994e"><strong>Real-World Analogies</strong></span>

Cloud service models can be compared to **food preparation options**.

| Model | Analogy                                         |
| ----- | ----------------------------------------------- |
| IaaS  | Buying raw ingredients and cooking yourself     |
| PaaS  | Meal kit delivery with pre-prepared ingredients |
| SaaS  | Ordering food from a restaurant                 |

Example workflow:

```text
IaaS → Build everything yourself
PaaS → Build only the application
SaaS → Just use the software
```

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of cloud services as **levels of responsibility**.

```text
IaaS → You manage most things
PaaS → You manage only application
SaaS → Provider manages everything
```

Example stack:

```text
Infrastructure → Platform → Software
```

Key idea:

> **Cloud service models determine how much of the computing stack is managed by the provider versus the user.**

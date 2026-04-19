
# <span style="color:#a7c957"><strong>Types of Client–Server Architecture (1-Tier, 2-Tier, 3-Tier)</strong></span>

Below is a **clear structural explanation of how client–server systems are organized into tiers**.
A **tier** represents a **logical layer responsible for a specific function** in the system.

Think of tiers as:

> **Separate layers that divide responsibilities such as user interface, application logic, and data storage.**

---

## 🔗 Navigation (H2 Anchors)

* [#tiers](#tiers) — **What “Tier” Means**
* [#one-tier](#one-tier) — **1-Tier Architecture**
* [#two-tier](#two-tier) — **2-Tier Architecture**
* [#three-tier](#three-tier) — **3-Tier Architecture**
* [#comparison](#comparison) — **Comparison of 1-Tier, 2-Tier, 3-Tier**
* [#constraints](#constraints) — **Constraints**
* [#failure-points](#failure-points) — **Failure Points**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="tiers"></a> <span style="color:#6a994e"><strong>What “Tier” Means</strong></span>

A **tier** refers to a **separate layer in the system architecture** responsible for a particular function.

Common system layers include:

| Layer              | Purpose        |
| ------------------ | -------------- |
| Presentation Layer | User interface |
| Application Layer  | Business logic |
| Data Layer         | Data storage   |

When we classify architectures like **1-tier, 2-tier, or 3-tier**, we are describing:

> **How these responsibilities are distributed across systems.**

---

# <a id="one-tier"></a> <span style="color:#6a994e"><strong>1-Tier Architecture</strong></span>

In **1-Tier Architecture**, everything runs on **one single system**.

All components are combined:

* User interface
* Business logic
* Database

Structure:

```text
Application
   │
UI + Logic + Database
(all in one system)
```

Example:

```text
Standalone Desktop Application
```

Example programs:

* Microsoft Access
* Simple offline accounting software
* Local database tools

Workflow:

```text
User interacts with application
↓
Application processes logic
↓
Data stored locally
```

Characteristics:

| Feature     | Description  |
| ----------- | ------------ |
| Network     | Not required |
| Deployment  | Very simple  |
| Scalability | Very limited |

Advantages:

* simple architecture
* fast execution
* no network dependency

Limitations:

* difficult to scale
* limited collaboration
* data centralized on one device

---

# <a id="two-tier"></a> <span style="color:#6a994e"><strong>2-Tier Architecture</strong></span>

In **2-Tier Architecture**, the system is divided into:

1. **Client**
2. **Server**

Structure:

```text
Client
   │
Application Logic + UI
   │
Network
   │
Database Server
```

The client communicates directly with the **database server**.

Example architecture:

```text
Desktop App → Database Server
```

Example systems:

* Banking internal software
* Enterprise desktop tools
* SQL client tools

Workflow:

```text
Client sends database query
↓
Database server processes query
↓
Server returns data
```

Example query:

```text
SELECT * FROM users;
```

Characteristics:

| Feature       | Description                |
| ------------- | -------------------------- |
| Architecture  | Client + Database          |
| Network       | Required                   |
| Communication | Direct database connection |

Advantages:

* faster than web systems
* simple architecture
* easy implementation

Limitations:

* limited scalability
* heavy load on database
* security challenges

---

# <a id="three-tier"></a> <span style="color:#6a994e"><strong>3-Tier Architecture</strong></span>

In **3-Tier Architecture**, the system is divided into **three layers**:

1. **Presentation Layer (Client)**
2. **Application Layer (Server)**
3. **Data Layer (Database)**

Structure:

```text
Client (UI)
   │
Application Server
   │
Database Server
```

Each tier performs a specific role.

Architecture diagram:

```text
User Browser
      │
      ▼
Web Server / API
      │
      ▼
Database Server
```

Workflow:

```text
Client sends request
↓
Application server processes logic
↓
Application server queries database
↓
Database returns data
↓
Application server sends response to client
```

Example system:

```text
Web Browser → Backend API → Database
```

Examples:

* modern web applications
* e-commerce platforms
* banking systems
* SaaS platforms

Characteristics:

| Feature     | Description            |
| ----------- | ---------------------- |
| Separation  | Clear layer separation |
| Security    | Improved               |
| Scalability | High                   |

Advantages:

* scalable
* maintainable
* secure
* flexible

Limitations:

* more complex
* requires network infrastructure
* higher development cost

---

# <a id="comparison"></a> <span style="color:#6a994e"><strong>Comparison of 1-Tier, 2-Tier, 3-Tier</strong></span>

| Feature       | 1-Tier        | 2-Tier                  | 3-Tier                          |
| ------------- | ------------- | ----------------------- | ------------------------------- |
| Layers        | Single system | Client + Database       | Client + Application + Database |
| Network       | Not required  | Required                | Required                        |
| Scalability   | Very low      | Medium                  | High                            |
| Complexity    | Low           | Medium                  | High                            |
| Security      | Low           | Medium                  | High                            |
| Typical usage | Local apps    | Enterprise desktop apps | Web applications                |

---

# <a id="constraints"></a> <span style="color:#6a994e"><strong>Constraints</strong></span>

Tiered architectures have several constraints.

### **1. Increased Complexity**

More tiers introduce:

* additional infrastructure
* network dependencies

---

### **2. Latency**

Each layer introduces communication delays.

Example:

```text
Client → Server → Database → Server → Client
```

---

### **3. Deployment Overhead**

Multiple tiers require:

* separate servers
* network configuration
* load balancing

---

# <a id="failure-points"></a> <span style="color:#6a994e"><strong>Failure Points</strong></span>

Common failure points include:

### **1. Server Failure**

If the application server fails:

```text
Clients cannot access services
```

---

### **2. Database Failure**

Database failure affects the entire system.

---

### **3. Network Failure**

Communication between tiers breaks.

---

### **4. Load Overload**

High user traffic can overload servers.

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of tiered architecture like a **restaurant system**.

| System Layer       | Restaurant Analogy |
| ------------------ | ------------------ |
| Client             | Customer           |
| Application Server | Waiter             |
| Database Server    | Kitchen            |

Flow:

```text
Customer places order
↓
Waiter processes request
↓
Kitchen prepares food
↓
Waiter delivers food
↓
Customer receives order
```

Mapping to software:

```text
Client sends request
↓
Application server processes logic
↓
Database stores or retrieves data
↓
Response sent back to client
```

The key idea:

> **Higher-tier architectures separate responsibilities to improve scalability, maintainability, and reliability.**

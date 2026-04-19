
# <span style="color:#a7c957"><strong>Layers of DNS (How Domain Name Resolution Works Internally)</strong></span>

DNS resolution follows a **hierarchical layered architecture**.
Each layer is responsible for **directing the query closer to the server that knows the final IP address**.

Think of DNS layers as:

> **A hierarchical lookup system where each layer knows where to find the next layer until the final IP address is discovered.**

---

## 🔗 Navigation (H2 Anchors)

* [#overview](#overview) — **Overview of DNS Layers**
* [#localdns](#localdns) — **Local DNS Resolver**
* [#root](#root) — **Root Name Server**
* [#tld](#tld) — **Top Level Domain (TLD) Server**
* [#nameserver](#nameserver) — **Authoritative Name Server**
* [#soa](#soa) — **SOA Record (Start of Authority)**
* [#full-example](#full-example) — **Complete DNS Resolution Example**
* [#communication](#communication) — **How Each Layer Communicates**
* [#analogy](#analogy) — **Real World Analogy**

---

# <a id="overview"></a> <span style="color:#6a994e"><strong>Overview of DNS Layers</strong></span>

DNS works using **five logical layers**.

Hierarchy:

```text
Client
  │
  ▼
Local DNS Resolver
  │
  ▼
Root Name Server
  │
  ▼
Top Level Domain (TLD) Server
  │
  ▼
Authoritative Name Server
  │
  ▼
SOA / DNS Records
```

Each layer performs **a narrowing search** for the domain.

Example lookup:

```text
app.example.com → 203.0.113.25
```

---

# <a id="localdns"></a> <span style="color:#6a994e"><strong>1. Local DNS Resolver</strong></span>

The **Local DNS resolver** is the first component involved in DNS resolution.

It usually belongs to:

* ISP
* Corporate network
* Public DNS provider

Examples:

* Google DNS (8.8.8.8)
* Cloudflare DNS (1.1.1.1)

### Function

The resolver performs **recursive DNS queries** on behalf of the client.

Process:

```text
Client asks local DNS:
"What is the IP of app.example.com?"
```

If cached:

```text
Return IP immediately
```

If not cached:

```text
Start DNS hierarchy search
```

### Role

The local DNS resolver **coordinates the entire resolution process**.

---

# <a id="root"></a> <span style="color:#6a994e"><strong>2. Root Name Server</strong></span>

The **Root Name Servers** sit at the top of the DNS hierarchy.

There are **13 logical root server clusters globally**.

Example root servers:

```text
a.root-servers.net
b.root-servers.net
```

### Function

Root servers **do not know the final IP address**.

Instead they answer:

```text
Which TLD server manages this domain?
```

Example query:

```text
Where is app.example.com?
```

Response:

```text
Ask the .com TLD server
```

Root servers direct the query **to the correct domain registry layer**.

---

# <a id="tld"></a> <span style="color:#6a994e"><strong>3. Top Level Domain (TLD) Server</strong></span>

The **TLD server manages domain extensions** such as:

| TLD  | Example        |
| ---- | -------------- |
| .com | google.com     |
| .org | wikipedia.org  |
| .net | cloudflare.net |
| .io  | github.io      |

### Function

The TLD server identifies:

```text
Which authoritative server manages the domain
```

Example query:

```text
Where is example.com?
```

Response:

```text
Ask the authoritative name server
```

The TLD server does **not provide the final IP**.

It directs the query to the **domain's DNS provider**.

---

# <a id="nameserver"></a> <span style="color:#6a994e"><strong>4. Authoritative Name Server</strong></span>

The **Authoritative Name Server** is responsible for a specific domain.

Example domain:

```text
example.com
```

The authoritative server contains **all DNS records for that domain**.

Example records:

```text
example.com
app.example.com
api.example.com
mail.example.com
```

### Function

The authoritative server answers:

```text
What is the IP address of this domain?
```

Example response:

```text
app.example.com → 203.0.113.25
```

This is the **final DNS resolution step**.

---

# <a id="soa"></a> <span style="color:#6a994e"><strong>5. SOA Record (Start of Authority)</strong></span>

The **SOA record** defines the **primary DNS configuration for a domain**.

Example SOA record:

```text
example.com SOA
Primary NS: ns1.exampledns.com
Admin email: admin@example.com
TTL: 3600
```

### Function

SOA provides metadata about:

* primary DNS server
* domain administrator
* refresh intervals
* replication timing

SOA ensures **DNS consistency across multiple name servers**.

---

# <a id="full-example"></a> <span style="color:#6a994e"><strong>Complete DNS Resolution Example</strong></span>

User enters:

```text
https://app.example.com
```

### Step 1 — Browser → Local DNS

```text
What is IP of app.example.com?
```

---

### Step 2 — Local DNS → Root Server

Root response:

```text
Ask the .com TLD server
```

---

### Step 3 — Local DNS → TLD Server

Query:

```text
Where is example.com?
```

Response:

```text
Ask authoritative name server
```

---

### Step 4 — Local DNS → Authoritative Server

Query:

```text
What is IP of app.example.com?
```

Response:

```text
203.0.113.25
```

---

### Step 5 — Local DNS → Client

The resolver returns:

```text
app.example.com → 203.0.113.25
```

The browser can now connect to the server.

---

# <a id="communication"></a> <span style="color:#6a994e"><strong>How Each Layer Communicates</strong></span>

DNS layers communicate using the **DNS protocol over UDP or TCP**.

Typical DNS request flow:

```text
Client → Resolver
Resolver → Root
Resolver → TLD
Resolver → Authoritative
Resolver → Client
```

DNS communication typically occurs on:

```text
Port 53
```

---

# <a id="analogy"></a> <span style="color:#6a994e"><strong>Real World Analogy</strong></span>

Think of DNS like **finding a person in a global directory system**.

Structure:

```text
Person → City Directory → State Registry → National Registry → Person Address
```

Mapping:

| DNS Layer            | Real World Equivalent  |
| -------------------- | ---------------------- |
| Local DNS            | Local phonebook        |
| Root Server          | Global directory       |
| TLD Server           | Country directory      |
| Authoritative Server | City directory         |
| SOA                  | Official record keeper |

Example flow:

```text
You search for John in your phonebook
↓
Phonebook tells you which city directory to check
↓
City directory tells you which street
↓
Street directory gives the house address
```

Similarly in DNS:

```text
Client → Local DNS → Root → TLD → Authoritative → IP Address
```

---

## Key Insight

The DNS system works efficiently because:

* **queries are cached**
* **hierarchy distributes load**
* **only authoritative servers store final records**

This design allows the internet to **resolve billions of domain requests every day efficiently**.

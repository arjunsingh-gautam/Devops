
# <span style="color:#a7c957"><strong>Network Protocols in the Application Layer (HTTP, HTTPS, SSH, RDP)</strong></span>

In networking, **protocols define the rules by which systems communicate**.
At the top of the networking stack lies the **Application Layer**, where user-facing services such as web browsing, remote login, and remote desktop operate.

Think of protocols as:

> **Standardized communication languages that allow applications running on different machines to exchange data reliably.**

---

## 🔗 Navigation (H2 Anchors)

* [#protocol-definition](#protocol-definition) — **What a Network Protocol Is**
* [#application-layer](#application-layer) — **Application Layer in Networking**
* [#http](#http) — **HTTP Protocol**
* [#https](#https) — **HTTPS Protocol**
* [#https-security](#https-security) — **What Makes HTTPS Secure**
* [#ssh](#ssh) — **SSH Protocol**
* [#rdp](#rdp) — **RDP Protocol**
* [#comparison](#comparison) — **Protocol Comparison**
* [#communication-flow](#communication-flow) — **How These Protocols Work Internally**
* [#security](#security) — **Security Considerations**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="protocol-definition"></a> <span style="color:#6a994e"><strong>What a Network Protocol Is</strong></span>

A **network protocol** is a **set of rules that defines how data is transmitted between devices over a network**.

Protocols define:

* message format
* communication sequence
* error handling
* data encoding

Example communication:

```text
Client → Request → Server
Server → Response → Client
```

Without protocols, systems would not know:

```text
How to structure messages
How to interpret incoming data
```

---

# <a id="application-layer"></a> <span style="color:#6a994e"><strong>Application Layer in Networking</strong></span>

The **application layer** is the highest layer in networking models like **OSI or TCP/IP**.

It provides protocols that enable **end-user services**.

Common application layer protocols include:

| Protocol | Purpose                     |
| -------- | --------------------------- |
| HTTP     | Web communication           |
| HTTPS    | Secure web communication    |
| SSH      | Secure remote server access |
| RDP      | Remote desktop access       |
| FTP      | File transfer               |
| DNS      | Domain resolution           |

Architecture example:

```text
User Application
      │
Application Layer Protocol
      │
Transport Layer (TCP/UDP)
      │
Network Layer (IP)
```

---

# <a id="http"></a> <span style="color:#6a994e"><strong>HTTP (HyperText Transfer Protocol)</strong></span>

HTTP is the **primary protocol used for web communication**.

Port used:

```text
80
```

Example request:

```text
GET /index.html HTTP/1.1
Host: example.com
```

### Characteristics

| Feature             | Description                       |
| ------------------- | --------------------------------- |
| Stateless           | Each request independent          |
| Text-based          | Human-readable headers            |
| Client-server model | Browser requests, server responds |

Example workflow:

```text
Browser → HTTP request → Web Server
Web Server → HTTP response → Browser
```

### Problem

HTTP is **not encrypted**.

This means:

```text
Data can be intercepted by attackers
```

Example:

```text
Login credentials transmitted in plain text
```

---

# <a id="https"></a> <span style="color:#6a994e"><strong>HTTPS (HyperText Transfer Protocol Secure)</strong></span>

HTTPS is the **secure version of HTTP**.

Port used:

```text
443
```

Structure:

```text
HTTPS = HTTP + TLS Encryption
```

Example connection:

```text
https://example.com
```

HTTPS ensures:

| Security Property | Meaning                          |
| ----------------- | -------------------------------- |
| Encryption        | Data cannot be read by attackers |
| Authentication    | Server identity verified         |
| Integrity         | Data cannot be modified          |

Example request:

```text
Encrypted HTTP request
```

---

# <a id="https-security"></a> <span style="color:#6a994e"><strong>What Makes HTTPS Secure</strong></span>

HTTPS uses **TLS (Transport Layer Security)**.

Security is achieved through several mechanisms.

---

### TLS Handshake

Before data transfer begins, a secure connection is established.

Handshake process:

```text
Client → Hello message
Server → Certificate
Client → Verify certificate
Client + Server → Generate encryption keys
```

---

### Encryption

Data is encrypted using symmetric encryption.

Example algorithms:

* AES
* ChaCha20

Result:

```text
Plain data → Encrypted data
```

Even if intercepted, attackers cannot read it.

---

### Authentication

Servers present a **digital certificate** issued by a trusted certificate authority.

Example certificate issuer:

* DigiCert
* Let's Encrypt
* GlobalSign

Browser verifies the certificate.

If invalid:

```text
Browser shows security warning
```

---

### Data Integrity

TLS ensures transmitted data cannot be altered.

Example:

```text
Hash verification
```

---

# <a id="ssh"></a> <span style="color:#6a994e"><strong>SSH (Secure Shell)</strong></span>

SSH is used for **secure remote login to servers**.

Port used:

```text
22
```

Example use:

```bash
ssh user@server-ip
```

Example:

```bash
ssh admin@203.0.113.25
```

### Purpose

SSH allows:

* remote server access
* command execution
* secure file transfer

Example workflow:

```text
Client → SSH authentication
Server → Secure terminal session
```

Security features:

* encrypted communication
* key-based authentication
* secure tunneling

Common use in DevOps:

```text
Server management
Deployment operations
Infrastructure automation
```

---

# <a id="rdp"></a> <span style="color:#6a994e"><strong>RDP (Remote Desktop Protocol)</strong></span>

RDP allows **remote graphical access to another computer**.

Port used:

```text
3389
```

Example usage:

```text
Remote login to Windows server
```

Instead of command-line access (like SSH), RDP provides:

```text
Full graphical desktop interface
```

Example architecture:

```text
Client Computer
      │
RDP Connection
      │
Remote Windows Server
```

Use cases:

* remote administration
* IT support
* remote work environments

---

# <a id="comparison"></a> <span style="color:#6a994e"><strong>Protocol Comparison</strong></span>

| Protocol | Port | Purpose                  | Security          |
| -------- | ---- | ------------------------ | ----------------- |
| HTTP     | 80   | Web communication        | No encryption     |
| HTTPS    | 443  | Secure web communication | TLS encryption    |
| SSH      | 22   | Remote server access     | Encrypted         |
| RDP      | 3389 | Remote desktop access    | Encrypted session |

---

# <a id="communication-flow"></a> <span style="color:#6a994e"><strong>How These Protocols Work Internally</strong></span>

Example HTTPS request flow:

```text
Browser
   │
DNS resolution
   │
TCP connection (port 443)
   │
TLS handshake
   │
HTTP request sent
   │
Web server processes request
   │
Encrypted response returned
```

Example SSH session:

```text
Client
   │
TCP connection (port 22)
   │
Authentication
   │
Encrypted terminal session
```

Example RDP session:

```text
Client
   │
TCP connection (port 3389)
   │
Authentication
   │
Remote desktop session
```

---

# <a id="security"></a> <span style="color:#6a994e"><strong>Security Considerations</strong></span>

These protocols have security implications.

Examples:

| Risk                       | Protocol                |
| -------------------------- | ----------------------- |
| Credential interception    | HTTP                    |
| Brute-force login attempts | SSH                     |
| RDP exploitation           | RDP exposed to internet |

Security best practices:

* disable unused ports
* use firewall rules
* require strong authentication

Example firewall rule:

```text
Allow: HTTPS (443)
Allow: SSH (22) from trusted IP
Block: RDP from public internet
```

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of protocols as **different communication methods with a building**.

| Protocol | Analogy                           |
| -------- | --------------------------------- |
| HTTP     | Sending an open postcard          |
| HTTPS    | Sending a sealed encrypted letter |
| SSH      | Secure maintenance entrance       |
| RDP      | Remote control of entire office   |

Example communication:

```text
Client chooses protocol
↓
Connects to server port
↓
Server processes request
↓
Response returned
```

The key idea:

> **Application-layer protocols define how specific services such as web browsing, remote login, and remote desktop operate across network connections.**

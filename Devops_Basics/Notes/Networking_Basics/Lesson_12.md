
# <span style="color:#a7c957"><strong>TCP and UDP — Core Transport Layer Protocols</strong></span>

In networking, **TCP and UDP are transport layer protocols responsible for moving data between devices across a network**.

They operate **above IP (Internet Protocol)** and **below application protocols like HTTP, HTTPS, SSH, etc.**

Think of them as:

> **The transport mechanisms that determine how data packets are delivered between two machines.**

---

## 🔗 Navigation (H2 Anchors)

* [#transport-layer](#transport-layer) — **Transport Layer Role**
* [#tcp](#tcp) — **What TCP Is**
* [#tcp-working](#tcp-working) — **How TCP Works**
* [#tcp-mechanics](#tcp-mechanics) — **Complete TCP Communication Mechanics**
* [#tcp-https](#tcp-https) — **How TCP Enables HTTPS**
* [#udp](#udp) — **What UDP Is**
* [#udp-working](#udp-working) — **How UDP Works**
* [#udp-problems](#udp-problems) — **Problems with UDP**
* [#tcp-vs-udp](#tcp-vs-udp) — **TCP vs UDP Comparison**
* [#usecases](#usecases) — **Where TCP and UDP Are Used**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="transport-layer"></a> <span style="color:#6a994e"><strong>Transport Layer Role</strong></span>

The transport layer sits between:

```text
Application Layer
Transport Layer (TCP / UDP)
Network Layer (IP)
```

Its responsibilities include:

| Responsibility  | Description                    |
| --------------- | ------------------------------ |
| Data delivery   | Send data between applications |
| Port management | Identify application endpoints |
| Reliability     | Ensure correct packet delivery |
| Flow control    | Prevent network congestion     |

The transport layer determines **how data packets are delivered**.

---

# <a id="tcp"></a> <span style="color:#6a994e"><strong>What TCP Is</strong></span>

TCP stands for:

```text
Transmission Control Protocol
```

It is a **connection-oriented protocol designed for reliable communication**.

Key features:

| Feature           | Description               |
| ----------------- | ------------------------- |
| Reliable delivery | Ensures packets arrive    |
| Ordered delivery  | Maintains packet order    |
| Error detection   | Detects corrupted packets |
| Retransmission    | Resends lost packets      |

TCP ensures **accurate and reliable data transfer**.

---

# <a id="tcp-working"></a> <span style="color:#6a994e"><strong>How TCP Works</strong></span>

TCP establishes a **connection between client and server before sending data**.

This is called the **three-way handshake**.

---

### TCP Handshake

Connection establishment process:

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

Explanation:

| Step    | Meaning                     |
| ------- | --------------------------- |
| SYN     | Client requests connection  |
| SYN-ACK | Server acknowledges request |
| ACK     | Client confirms connection  |

After this process:

```text
Connection established
```

Data transmission can begin.

---

# <a id="tcp-mechanics"></a> <span style="color:#6a994e"><strong>Complete TCP Communication Mechanics</strong></span>

Example scenario: accessing a website.

---

### Step 1 — Client sends request

Browser initiates connection to server.

Example:

```text
Client → ServerIP:443
```

---

### Step 2 — TCP handshake

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

Connection established.

---

### Step 3 — Data segmentation

Application data is broken into TCP segments.

Example:

```text
Segment 1
Segment 2
Segment 3
```

Each segment contains:

```text
Sequence number
Acknowledgment number
Payload
```

---

### Step 4 — Data transmission

Segments are sent through the network.

Routers forward packets to destination.

---

### Step 5 — Packet ordering

Receiver reconstructs packets using sequence numbers.

Example:

```text
Received: 3, 1, 2
Reordered: 1, 2, 3
```

---

### Step 6 — Acknowledgement

Receiver confirms packet receipt.

Example:

```text
ACK 3
```

Meaning:

```text
Packets up to sequence 3 received
```

---

### Step 7 — Retransmission

If packets are missing:

```text
Sender retransmits lost packets
```

This ensures **reliable communication**.

---

# <a id="tcp-https"></a> <span style="color:#6a994e"><strong>How TCP Enables HTTPS</strong></span>

HTTPS operates **on top of TCP**.

Communication stack:

```text
Application: HTTPS
Transport: TCP
Network: IP
```

Connection process:

```text
Browser
   │
TCP Connection
   │
TLS Handshake
   │
Encrypted HTTP Communication
```

Why TCP is required:

| Requirement           | TCP Role                   |
| --------------------- | -------------------------- |
| Reliable delivery     | Prevent packet loss        |
| Ordered data          | Maintain encryption stream |
| Connection management | Maintain session state     |

Without TCP:

```text
TLS encryption would break due to unordered packets
```

Therefore HTTPS depends on **TCP reliability**.

---

# <a id="udp"></a> <span style="color:#6a994e"><strong>What UDP Is</strong></span>

UDP stands for:

```text
User Datagram Protocol
```

It is a **connectionless protocol designed for fast data transmission**.

Key characteristics:

| Feature                  | Description                     |
| ------------------------ | ------------------------------- |
| No connection            | No handshake                    |
| No reliability guarantee | Packets may be lost             |
| No ordering              | Packets may arrive out of order |
| Minimal overhead         | Faster transmission             |

UDP prioritizes **speed over reliability**.

---

# <a id="udp-working"></a> <span style="color:#6a994e"><strong>How UDP Works</strong></span>

UDP sends packets directly without establishing a connection.

Process:

```text
Sender → Send packet
Receiver → Receive packet
```

No handshake occurs.

Example UDP packet structure:

```text
Source Port
Destination Port
Length
Checksum
Payload
```

Once sent:

```text
Packet may arrive or be lost
```

Sender does not verify delivery.

---

# <a id="udp-problems"></a> <span style="color:#6a994e"><strong>Problems with UDP</strong></span>

UDP sacrifices reliability.

Major limitations include:

---

### Packet Loss

UDP does not retransmit lost packets.

Example:

```text
Packet 4 lost
```

Transmission continues without recovery.

---

### Packet Reordering

Packets may arrive out of order.

Example:

```text
Received packets: 2, 1, 3
```

Application must handle reordering.

---

### No Congestion Control

UDP does not manage network congestion.

This may cause:

```text
Network overload
```

---

### No Acknowledgment

Sender never knows if data was received.

---

# <a id="tcp-vs-udp"></a> <span style="color:#6a994e"><strong>TCP vs UDP Comparison</strong></span>

| Feature         | TCP                 | UDP            |
| --------------- | ------------------- | -------------- |
| Connection      | Connection-oriented | Connectionless |
| Reliability     | Guaranteed          | Not guaranteed |
| Packet ordering | Maintained          | Not guaranteed |
| Error recovery  | Yes                 | No             |
| Speed           | Slower              | Faster         |
| Overhead        | Higher              | Lower          |

---

# <a id="usecases"></a> <span style="color:#6a994e"><strong>Where TCP and UDP Are Used</strong></span>

### TCP Use Cases

Used when reliability is required.

Examples:

| Application   | Reason                  |
| ------------- | ----------------------- |
| HTTP/HTTPS    | Reliable page loading   |
| Email         | Data integrity required |
| File transfer | Accurate data transfer  |

---

### UDP Use Cases

Used when **low latency is more important than reliability**.

Examples:

| Application     | Reason                    |
| --------------- | ------------------------- |
| Video streaming | Dropped frames acceptable |
| Online gaming   | Fast response required    |
| DNS queries     | Lightweight requests      |
| VoIP calls      | Low latency communication |

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of TCP and UDP like **two types of delivery services**.

| Protocol | Analogy                                       |
| -------- | --------------------------------------------- |
| TCP      | Registered courier with delivery confirmation |
| UDP      | Standard postal drop without confirmation     |

Example delivery:

TCP:

```text
Send package
↓
Receiver confirms delivery
↓
If lost → resend package
```

UDP:

```text
Send package
↓
No confirmation
↓
If lost → sender unaware
```

Key idea:

> **TCP prioritizes reliability and accuracy, while UDP prioritizes speed and low overhead.**

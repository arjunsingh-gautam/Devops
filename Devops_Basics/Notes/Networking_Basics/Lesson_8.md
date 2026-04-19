
# <span style="color:#a7c957"><strong>Important Linux Networking Commands for DevOps Engineers</strong></span>

Linux networking commands are **essential tools for debugging connectivity, diagnosing infrastructure issues, and inspecting system network state**.

In DevOps, these commands help you answer questions like:

* Is the server reachable?
* Is the service listening on the correct port?
* Is DNS resolving correctly?
* Where is the network failing?

Think of them as:

> **Diagnostic instruments for observing and troubleshooting network behavior in systems and infrastructure.**

---

## 🔗 Navigation (H2 Anchors)

* [#categories](#categories) — **Categories of Linux Network Commands**
* [#ip](#ip) — **ip Command**
* [#ping](#ping) — **ping**
* [#traceroute](#traceroute) — **traceroute**
* [#nslookup](#nslookup) — **nslookup**
* [#dig](#dig) — **dig**
* [#curl](#curl) — **curl**
* [#netstat](#netstat) — **netstat**
* [#ss](#ss) — **ss**
* [#lsof](#lsof) — **lsof**
* [#nc](#nc) — **nc (netcat)**
* [#tcpdump](#tcpdump) — **tcpdump**
* [#ifconfig](#ifconfig) — **ifconfig**
* [#usecases](#usecases) — **Common DevOps Debugging Scenarios**
* [#mental-model](#mental-model) — **Simple Mental Model**

---

# <a id="categories"></a> <span style="color:#6a994e"><strong>Categories of Linux Network Commands</strong></span>

Networking commands fall into several categories.

| Category              | Purpose                      |
| --------------------- | ---------------------------- |
| Connectivity testing  | Check if hosts are reachable |
| DNS debugging         | Verify domain resolution     |
| Port inspection       | Check open services          |
| Traffic monitoring    | Inspect packets              |
| Network configuration | View interfaces              |

DevOps engineers use these commands for **production debugging and infrastructure monitoring**.

---

# <a id="ip"></a> <span style="color:#6a994e"><strong>ip Command</strong></span>

The `ip` command is the **modern Linux tool for managing network interfaces and routing**.

### Check IP address

```bash
ip addr
```

Example output:

```text
eth0: 192.168.1.20
```

### Check routing table

```bash
ip route
```

Example:

```text
default via 192.168.1.1
```

### Use Case in DevOps

Used to verify:

* server IP configuration
* network interface status
* routing rules

---

# <a id="ping"></a> <span style="color:#6a994e"><strong>ping</strong></span>

`ping` tests **network connectivity between two machines**.

Example:

```bash
ping google.com
```

Output:

```text
64 bytes from 142.250.190.78: icmp_seq=1 ttl=117 time=12 ms
```

Purpose:

* verify host reachability
* measure latency
* detect packet loss

DevOps use case:

```text
Check if production server is reachable
```

---

# <a id="traceroute"></a> <span style="color:#6a994e"><strong>traceroute</strong></span>

`traceroute` shows **the path packets take across the network**.

Example:

```bash
traceroute google.com
```

Output:

```text
Router1 → Router2 → ISP → Destination
```

Purpose:

* identify network bottlenecks
* locate routing failures

DevOps use case:

```text
Debug slow external API connectivity
```

---

# <a id="nslookup"></a> <span style="color:#6a994e"><strong>nslookup</strong></span>

`nslookup` queries **DNS servers for domain resolution**.

Example:

```bash
nslookup google.com
```

Output:

```text
google.com → 142.250.190.78
```

Purpose:

* check DNS resolution
* debug DNS issues

DevOps scenario:

```text
Check if domain resolves to correct load balancer IP
```

---

# <a id="dig"></a> <span style="color:#6a994e"><strong>dig</strong></span>

`dig` (Domain Information Groper) provides **detailed DNS query results**.

Example:

```bash
dig google.com
```

Output shows:

* DNS records
* query time
* authoritative server

Example query for specific record:

```bash
dig example.com A
```

DevOps use case:

```text
Verify DNS propagation after infrastructure changes
```

---

# <a id="curl"></a> <span style="color:#6a994e"><strong>curl</strong></span>

`curl` sends **HTTP requests from the command line**.

Example:

```bash
curl https://api.example.com
```

Output:

```text
API response data
```

Useful options:

```bash
curl -I https://example.com
```

Shows headers.

DevOps use case:

```text
Test API endpoints
Check server responses
```

---

# <a id="netstat"></a> <span style="color:#6a994e"><strong>netstat</strong></span>

`netstat` displays **network connections and listening ports**.

Example:

```bash
netstat -tuln
```

Output:

```text
tcp   0   0   0.0.0.0:80   LISTEN
```

Meaning:

```text
Web server listening on port 80
```

DevOps use case:

```text
Verify service is running on correct port
```

---

# <a id="ss"></a> <span style="color:#6a994e"><strong>ss</strong></span>

`ss` is the **modern replacement for netstat**.

Example:

```bash
ss -tuln
```

Shows:

* open ports
* active connections

Example output:

```text
LISTEN 0 128 0.0.0.0:22
```

DevOps use case:

```text
Check SSH port status
```

---

# <a id="lsof"></a> <span style="color:#6a994e"><strong>lsof</strong></span>

`lsof` lists **processes using network ports**.

Example:

```bash
lsof -i :80
```

Output:

```text
nginx 1234 LISTEN
```

Purpose:

Identify **which application is using a port**.

DevOps scenario:

```text
Find process blocking port 443
```

---

# <a id="nc"></a> <span style="color:#6a994e"><strong>nc (netcat)</strong></span>

`nc` tests **port connectivity**.

Example:

```bash
nc -zv google.com 443
```

Output:

```text
Connection successful
```

Purpose:

Check if specific ports are open.

DevOps scenario:

```text
Verify database port accessibility
```

---

# <a id="tcpdump"></a> <span style="color:#6a994e"><strong>tcpdump</strong></span>

`tcpdump` captures **network packets in real time**.

Example:

```bash
tcpdump -i eth0
```

Shows packets flowing through the network interface.

Example filter:

```bash
tcpdump port 80
```

Use cases:

* debug network traffic
* inspect suspicious packets

DevOps scenario:

```text
Investigate production network issues
```

---

# <a id="ifconfig"></a> <span style="color:#6a994e"><strong>ifconfig</strong></span>

`ifconfig` shows **network interface configuration**.

Example:

```bash
ifconfig
```

Output:

```text
eth0 192.168.1.20
```

Note:

Modern Linux systems prefer:

```bash
ip addr
```

instead of `ifconfig`.

---

# <a id="usecases"></a> <span style="color:#6a994e"><strong>Common DevOps Debugging Scenarios</strong></span>

Example production troubleshooting workflow.

### Server unreachable

Commands:

```bash
ping server-ip
traceroute server-ip
```

---

### DNS issues

Commands:

```bash
nslookup domain.com
dig domain.com
```

---

### Service not responding

Commands:

```bash
ss -tuln
lsof -i :port
```

---

### API debugging

Command:

```bash
curl https://api.service.com
```

---

### Network packet inspection

Command:

```bash
tcpdump -i eth0
```

---

# <a id="mental-model"></a> <span style="color:#6a994e"><strong>Simple Mental Model</strong></span>

Think of Linux network commands like **diagnostic tools in a hospital**.

| Command    | Diagnostic Tool       |
| ---------- | --------------------- |
| ping       | Heartbeat monitor     |
| traceroute | X-ray of network path |
| curl       | API tester            |
| ss/netstat | Service port scanner  |
| tcpdump    | Packet microscope     |

DevOps engineers use them to **observe, diagnose, and repair network behavior in production systems**.

Key idea:

> **Linux networking commands provide visibility into connectivity, DNS resolution, service availability, and packet-level communication in distributed systems.**

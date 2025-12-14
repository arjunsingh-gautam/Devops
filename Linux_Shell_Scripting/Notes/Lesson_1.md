# <span style="color:#a2d2ff">**Lesson-1:EC2 Instance and SSH connection**</span>

## <span style="color:#ffb703">**What is SSH and SSH client and how to connect to our EC2 instance using a SSH clietn**</span>

### 🔐 **1. What is SSH?**

**SSH (Secure Shell)** is a cryptographic network protocol that allows secure communication between two systems over an unsecured network. It’s mainly used for:

- Remote login to machines (like EC2 instances).
- Secure file transfers (using `scp`, `sftp`).
- Executing commands on remote machines.

SSH **encrypts** the entire session — ensuring **confidentiality**, **integrity**, and **authenticity**.

---

### 💻 **2. What is an SSH Client?**

An **SSH client** is a program that initiates the connection to a remote machine using the SSH protocol.

### Examples:

| Platform    | Common SSH Clients                                                   |
| ----------- | -------------------------------------------------------------------- |
| Linux/macOS | `ssh` command in terminal                                            |
| Windows     | [PuTTY](https://www.putty.org/), Windows Terminal (recently), or WSL |
| GUI tools   | Termius, MobaXterm, Bitvise                                          |

> In AWS EC2 context, when we say **"connect to EC2 using SSH"**, we mean:
> "Use an SSH client to securely log into the EC2 virtual server hosted in AWS."

---

### 🌐 **3. How SSH Connects to EC2: Network Mechanics (in Detail)**

Let’s break down the process **step-by-step**:

---

### 🔑 Step 1: **Key Pair Generation**

When launching an EC2 instance, AWS allows you to **create or choose an existing key pair**:

- `.pem` file = your **private key**
- AWS stores the corresponding **public key** on the EC2 instance (specifically in `~/.ssh/authorized_keys` of the default user like `ec2-user`)

These keys follow **public-key cryptography** (e.g., RSA, ED25519).

---

### 🧩 Step 2: **Initiating SSH Connection**

From your machine (client), you run:

```bash
ssh -i my-key.pem ec2-user@<EC2-Public-IP>
```

- `-i my-key.pem`: specifies the **private key**
- `ec2-user`: default username for Amazon Linux
- `<EC2-Public-IP>`: the public IP assigned by AWS to your EC2 instance

---

### 🌍 Step 3: **Network Routing & DNS Resolution**

- Your client resolves `<EC2-Public-IP>` or `<ec2-xx-xx-xx-xx.compute.amazonaws.com>` using DNS.
- The TCP packet is constructed with:

  - Destination IP = EC2 instance public IP
  - Port = **22** (default for SSH)

- It travels over the internet using **TCP 3-way handshake** to establish connection.

---

### 🔐 Step 4: **Authentication and Encryption**

Once the TCP connection is established:

1. **SSH Handshake begins**:

   - The client and server exchange information about the encryption algorithms (cipher suites) they support.
   - They agree on a **session key** using methods like **Diffie-Hellman** or **ECDH**.

2. **Authentication**:

   - Server challenges the client to prove it owns the private key.
   - The client uses its `.pem` file (private key) to sign a message.
   - The server verifies the signature using the **public key** already stored on the EC2 machine.

✅ If valid → access is granted.

---

### 🔒 Step 5: **Encrypted Session Starts**

After authentication:

- All communication (terminal commands, output, etc.) is **encrypted using symmetric encryption** (AES, ChaCha20, etc.).
- Even if someone intercepts packets, they cannot read or tamper with data.

---

### ✅ Requirements for Successful SSH to EC2

1. **Correct Key Pair** (private key on your local machine, matching public key on EC2).
2. **Public IP or DNS Name** of the EC2 instance.
3. **Port 22 Open in Security Group**:

   - AWS Security Group must allow incoming TCP on port 22 **from your IP**.

4. **Running SSH Daemon on EC2**:

   - The EC2 instance must be running `sshd` (SSH server software).

5. **Correct Username**:

   - e.g., `ec2-user`, `ubuntu`, `admin`, etc., depending on the AMI.

---

## 🔁 Summary: SSH to EC2

```
You (Client) → [Encrypted SSH Packet via TCP Port 22] → EC2 Instance (Server)
```

- ✅ Secure
- ✅ Authenticated
- ✅ Encrypted
- ✅ Allows terminal/command-line access to remote server

---

![EC2_SSH connection](img/EC2_SSH.png)

## <span style="color:#ffb703">**What is a .pem file**</span>

### 🔑 **A `.pem` file is your SSH private key file**

It’s a **Plaintext file** that stores **cryptographic keys**, and in the case of AWS EC2, it contains your **private key** used for **authenticating via SSH**.

**PEM stands for**: _Privacy Enhanced Mail_ — it's a standard format for encoding keys and certificates.

---

### 🔐 Why is it important?

When you connect to an EC2 instance using SSH, AWS doesn't ask you for a **password**. Instead, it uses **public-key authentication**:

| Component                     | Stored Where                                    | Purpose                      |
| ----------------------------- | ----------------------------------------------- | ---------------------------- |
| **Public key**                | Stored inside EC2 (in `~/.ssh/authorized_keys`) | Used to verify your identity |
| **Private key** (`.pem` file) | Stored on your local machine                    | Used to prove your identity  |

---

### 🧠 What’s inside a `.pem` file?

It’s a text file that looks like this:

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAzNFxNlGm...
...lots of base64 text...
-----END RSA PRIVATE KEY-----
```

It encodes a **private key** (RSA or sometimes ED25519) in a Base64 format, wrapped with BEGIN/END lines.

---

### 💡 PEM file in AWS EC2

When you launch an EC2 instance and select a key pair:

- If you **create a new key pair**, AWS gives you a `.pem` file to **download only once**.
- That file lets you SSH into the EC2:

  ```bash
  ssh -i my-key.pem ec2-user@<EC2-Public-IP>
  ```

🔒 You must **protect** this file:

- Don’t share it.
- Don’t commit it to GitHub.
- Set strict permissions:

  ```bash
  chmod 400 my-key.pem
  ```

---

### 🚨 What if I lose my `.pem` file?

- You **cannot SSH into your EC2 anymore**.
- You'll have to:

  - Stop the instance,
  - Detach its volume,
  - Mount it to another instance,
  - Manually update the `.ssh/authorized_keys` file with a new public key.

**Or** just launch a new instance with a new key pair.

---

### 🔁 Summary

| Question              | Answer                                                                     |
| --------------------- | -------------------------------------------------------------------------- |
| What is `.pem`?       | A file that holds your SSH **private key**                                 |
| Used for?             | Authenticating your identity when connecting to EC2                        |
| File format?          | Base64-encoded text key in PEM format                                      |
| What happens if lost? | You’ll be locked out of the instance unless you recover access another way |

---

## <span style="color:#ffb703">**How to create an EC2 and connect it to your machine using SSH client**</span>

### 🟢 STEP 1: Launch EC2 Instance on AWS

1. **Login to your AWS account**
2. Go to the top search bar → Type **"EC2"** → Click on **EC2 (under Services)**
3. In the EC2 dashboard, click **“Launch Instance”**
4. Fill in these details:

   - **Name**: Choose any name (e.g., `my-first-ec2`)
   - **Amazon Machine Image (AMI)**: Choose OS, e.g., **Amazon Linux 2023**, **Ubuntu**, etc.
   - **Instance Type**: Choose **t2.micro** (eligible for free tier)
   - **Key Pair (login)**:

     - If you **don’t have one**, click **“Create new key pair”**

       - Name it (e.g., `my-key`)
       - Select **.pem** format
       - Click **Download Key Pair** (very important!)

     - If you already have one, select it

   - **Leave remaining settings as default**

5. Click **“Launch Instance”**

---

### 🟢 STEP 2: Locate Your Instance & Get Connection Info

1. Go to **Instances tab**
2. You’ll see your instance listed → Wait until its **State = Running**
3. Select the instance → Click **“Connect”**
4. Choose the **SSH tab**, it will show a command like:

   ```bash
   ssh -i "my-key.pem" ec2-user@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
   ```

---

### 🟢 STEP 3: Prepare the `.pem` File in Git Bash

1. Move the downloaded `.pem` file to a **safe folder**, e.g., `C:\Users\<YourName>\ec2-keys\my-key.pem`
2. Open **Git Bash**
3. Navigate to the folder:

   ```bash
   cd /c/Users/<YourName>/ec2-keys
   ```

4. Set correct permissions:

   ```bash
   chmod 400 my-key.pem
   ```

---

### 🟢 STEP 4: Connect to EC2 via Git Bash

Now use the SSH command shown in the AWS console:

```bash
ssh -i "my-key.pem" ec2-user@ec2-xx-xx-xx-xx.compute-1.amazonaws.com
```

💡 Replace:

- `"my-key.pem"` with your key file name
- `ec2-user@...` with your EC2 public DNS or IP

**You’re now inside a Linux machine!** 🎉 You can use terminal commands like `ls`, `cd`, `sudo yum install`, etc.

---

### 🔴 How to Stop (or Start) Your EC2 Instance

1. Go to the **Instances** tab
2. Select your instance
3. Click **“Instance State”** in the top menu
4. Choose **“Stop Instance”** (you can start it later anytime)

---

### 📌 Quick Summary

| Action                | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| **Key File (.pem)**   | Needed for SSH login. Keep it safe!                            |
| **chmod 400**         | Sets secure file permissions (read-only)                       |
| **SSH Command**       | Connect to EC2 via terminal                                    |
| **Stopping Instance** | Saves cost; you don’t pay for stopped instances (only storage) |

---

## <span style="color:#ffb703">**How to choose and OS image and instancy type of EC2 instance**</span>

### 🖥️ PART 1: Choosing the **OS Image (AMI)**

### ❓ What is an AMI?

**AMI (Amazon Machine Image)** is a pre-configured template of an operating system + optional software.

When launching an EC2 instance, you select an AMI to determine **which OS** (and tools) your virtual machine will have.

---

### 📦 Common AMIs & Their Use Cases:

| AMI Name                            | Description                                  | Default Username      | Use Case                                       |
| ----------------------------------- | -------------------------------------------- | --------------------- | ---------------------------------------------- |
| **Amazon Linux 2/2023**             | Lightweight, secure, AWS-optimized Linux     | `ec2-user`            | Best for general use, web hosting, learning    |
| **Ubuntu**                          | Popular open-source Linux distro             | `ubuntu`              | DevOps, Python/ML, Node.js apps                |
| **Red Hat Enterprise Linux (RHEL)** | Commercial enterprise Linux                  | `ec2-user`            | Corporate/Enterprise apps                      |
| **CentOS / Rocky Linux**            | Community-supported RHEL clones              | `centos` / `ec2-user` | Server setups, firewall/gateway systems        |
| **Debian**                          | Lightweight, stable Linux distro             | `admin` / `debian`    | Python, servers, data processing               |
| **Microsoft Windows Server**        | Windows OS with GUI                          | `Administrator`       | .NET apps, SQL Server, remote desktop          |
| **Deep Learning AMI**               | Ubuntu + Python + pre-installed ML libraries | `ubuntu`              | Machine Learning, TensorFlow, PyTorch, Jupyter |

---

### 🔍 How to Choose?

| If You Want To...                      | Choose This                         |
| -------------------------------------- | ----------------------------------- |
| Learn Linux, run basic servers         | Amazon Linux 2 or Ubuntu            |
| Work with Python, ML, or AI            | Ubuntu or Deep Learning AMI         |
| Host web apps (Node.js, Django, Flask) | Ubuntu or Amazon Linux              |
| Run Windows programs remotely          | Windows Server AMI                  |
| Use Red Hat in enterprise setting      | RHEL                                |
| Just explore SSH and terminal          | Amazon Linux 2 (Free Tier eligible) |

---

### ⚙️ PART 2: Choosing an **Instance Type**

### ❓ What is an Instance Type?

It defines the **hardware configuration** (CPU, RAM, network) of your virtual machine.

AWS offers many **families** of instance types optimized for different tasks.

---

### 🧩 Common Instance Families

| Family                              | Description                   | Best For                                 |
| ----------------------------------- | ----------------------------- | ---------------------------------------- |
| **t2 / t3 / t4g (General Purpose)** | Balanced CPU, memory, network | Basic workloads, practice, web servers   |
| **m5 / m6g (Compute + Memory)**     | More RAM and CPU              | Medium-sized apps, databases             |
| **c5 / c6g (Compute Optimized)**    | High CPU, lower RAM           | CPU-heavy tasks (encoding, ML inference) |
| **r5 / r6g (Memory Optimized)**     | Large RAM                     | In-memory DBs, analytics                 |
| **g4 / g5 (GPU)**                   | Comes with NVIDIA GPU         | ML training, graphics, gaming apps       |
| **i3 / i4 (Storage Optimized)**     | High-speed local SSDs         | NoSQL DBs, caching, real-time analytics  |

---

### ✅ Most Common for Beginners (Free Tier)

| Instance Type | Specs            | Cost      | Notes                                 |
| ------------- | ---------------- | --------- | ------------------------------------- |
| **t2.micro**  | 1 vCPU, 1 GB RAM | Free tier | Perfect for SSH practice, web hosting |
| **t3.micro**  | 2 vCPU, 1 GB RAM | Very low  | Slightly faster, cheap                |
| **t2.small**  | 1 vCPU, 2 GB RAM | Low       | Better for small apps                 |

> ⚠️ To stay in Free Tier: Use **Amazon Linux 2** + **t2.micro**

---

### 📌 How to Select During EC2 Launch

### In AWS EC2 Console:

1. After naming your instance → Click **“Choose AMI”**

   - Use filters like: “Quick Start”, “Ubuntu”, “Amazon Linux”, etc.

2. Click **“Choose Instance Type”**

   - Use the search bar → type `t2.micro`, `t3.micro`, etc.

---

### 🧠 Tips for Choosing:

- ✅ For basic learning / hosting a small app → `Amazon Linux 2` + `t2.micro`
- 🔍 Want Ubuntu/deb package access? → Use `Ubuntu 20.04` or `22.04`
- ⚡ Need a bit more power? → `t2.small` or `t3.micro`
- 💻 Doing GPU or ML? → Use **Deep Learning AMI** + `g4dn.xlarge` (not free)

---

### 🧾 Summary Table

| OS Image          | When to Use                            |
| ----------------- | -------------------------------------- |
| Amazon Linux      | AWS-optimized, fast boot, CLI-friendly |
| Ubuntu            | Dev-friendly, Python, ML, Node.js      |
| Windows Server    | GUI-based remote access                |
| Deep Learning AMI | Comes with preinstalled ML packages    |
| RHEL/CentOS       | Enterprise use                         |

| Instance Type | Specs                    | Use Case                     |
| ------------- | ------------------------ | ---------------------------- |
| t2.micro      | 1 vCPU, 1 GB RAM         | Free tier learning, SSH      |
| t2.small      | 1 vCPU, 2 GB RAM         | Slightly better RAM          |
| t3.micro      | 2 vCPU, 1 GB RAM         | Better burst CPU performance |
| g4dn.xlarge   | 1 GPU, 4 vCPU, 16 GB RAM | ML, AI training (paid)       |

---

## <span style="color:#ffb703">**What happens to your files when you stop the instance**</span>

### 🧠 The Core Concept:

### 🔁 When you **stop** an EC2 instance:

- **The virtual machine (VM)** (i.e., CPU, RAM, etc.) is released.
- But your **disk (storage)** remains **intact and persistent**.

This is made possible by something called **EBS (Elastic Block Store)**.

---

### 🧱 Think of EC2 Like This:

### 🧳 Analogy:

Imagine EC2 as a **rented laptop**:

- You can power it off and return the CPU and screen.
- But your **hard disk stays stored in a locker**, untouched.
- Next time you rent the laptop again, you re-attach the same hard disk, and **all your files are still there**.

In AWS terms:

| Component           | Real-World Equivalent             | What Happens on Stop                    |
| ------------------- | --------------------------------- | --------------------------------------- |
| EC2 instance (VM)   | The powered-on laptop (CPU + RAM) | Released to AWS pool                    |
| EBS volume          | The hard drive                    | Remains attached but powered down       |
| Public IP (default) | The internet plug                 | Might be lost unless Elastic IP is used |

---

### 🧱 EBS (Elastic Block Store): The Key Mechanism

### 🔹 What is EBS?

- EBS is **network-attached block storage**.
- Acts like a **virtual hard disk** for your EC2 instance.
- You can format it, create directories, store files — just like a normal disk.

### 🔸 Persistence:

- EBS volumes are **persistent** by default.
- When you stop or reboot your EC2 instance, the **EBS volume is preserved**.
- It continues to exist (and you continue to be billed for it).

---

### ⚙️ What Happens Internally When You Stop an EC2 Instance?

1. **CPU and RAM resources** are released by AWS.
2. **Your EBS root volume remains** in AWS storage infrastructure (like AWS S3/SSD-backed services).
3. When you restart:

   - AWS boots a **new VM** (could be on a different physical machine).
   - It **reattaches your EBS volume** to that new VM.
   - It then boots your OS from that disk — just like booting from a hard drive on a new machine.

4. Your data, files, installed packages, configurations — **all remain**.

---

### ☁️ Where Is Your Data Physically Stored?

- EBS volumes are stored in the **same Availability Zone (AZ)** as your EC2 instance.
- Backed by **durable SSDs**, with automatic replication across infrastructure within the AZ.
- AWS handles the **redundancy, durability, and failure recovery** of this data.

---

### ❗What If You “Terminate” the Instance?

- Stopping ≠ Terminating.

| Action                 | What Happens to Data                                                               |
| ---------------------- | ---------------------------------------------------------------------------------- |
| **Stop Instance**      | EBS volume is preserved                                                            |
| **Terminate Instance** | By default, root volume is **deleted** unless you uncheck that option during setup |

So, always be cautious before hitting “Terminate”.

---

### 📍Optional Add-ons for More Control

| Feature                  | Purpose                                                  |
| ------------------------ | -------------------------------------------------------- |
| **Elastic IP**           | Keeps the public IP fixed even after stop/start          |
| **Snapshot**             | Backup your EBS volume (stored in S3)                    |
| **Attach Extra Volumes** | Add more storage disks to EC2 (e.g., for database, logs) |

---

### ✅ Summary

| Component       | Behavior on Stop                     |
| --------------- | ------------------------------------ |
| CPU/RAM (VM)    | Released back to AWS pool            |
| EBS Volume      | Retained (persistent disk)           |
| Data inside EC2 | Remains safe inside EBS              |
| Public IP       | May change unless Elastic IP is used |

🧠 **This separation of Compute (EC2) and Storage (EBS)** is what enables AWS to offer flexible, scalable, and persistent cloud computing.

---

![EBS_working](img/EBS.png)

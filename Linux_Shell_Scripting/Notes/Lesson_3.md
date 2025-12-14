# <span style="color:#a2d2ff">**Lesson-3: Linux File System**</span>

## <span style="color:#ffb703">**Introduction to Linux File Systems**</span>

- Linux follows _unified I/O abstraction_: an resource you interact with is exposed as a file
- This means hardware devices,processes,network sockets, and data are all accessed using the same set of system calls(`open,read,write,close`)

---

## Why was this architecture chosen?

### 1. Simplicity (One Interface to Rule Them All)

Instead of learning different APIs for:

- Disk
- Keyboard
- Screen
- Network
- Processes

You use the **same file API** everywhere.

```c
read(fd, buffer, size);
```

Whether `fd` points to:

- a text file
- a keyboard
- a network socket
- a process stat file

---

### 2. Power of Composition (Unix Philosophy)

Small tools + files = powerful systems.

```bash
cat /proc/cpuinfo | grep MHz | sort
```

- `/proc/cpuinfo` → CPU info (not a real file!)
- `grep`, `sort` → generic file tools
  ➡️ works because **everything behaves like a file**

---

### 3. Hardware Independence

Applications don’t care _how_ data is produced.
They just **read/write bytes**.

Kernel handles:

- Disk drivers
- Keyboard drivers
- Network drivers

---

### 4. Security & Permissions

Same permission model:

- Who can read?
- Who can write?
- Who can execute?

Applies uniformly to:

- Files
- Devices
- Pipes
- Process info

---

### 5. Scalability & Extensibility

New devices or features → just expose a new file:

- `/proc`
- `/sys`
- `/dev`

No new APIs required.

---

## Types of Files in Linux (with examples)

Run:

```bash
ls -l
```

First character tells file type.

| Symbol | File Type         | Example                    | Explanation              |
| ------ | ----------------- | -------------------------- | ------------------------ |
| `-`    | Regular file      | `/etc/passwd`, `notes.txt` | Text, binary, executable |
| `d`    | Directory         | `/home`, `/etc`            | Holds files              |
| `c`    | Character device  | `/dev/tty`, `/dev/null`    | Stream devices           |
| `b`    | Block device      | `/dev/sda`, `/dev/nvme0n1` | Disk devices             |
| `l`    | Symbolic link     | `/bin/sh → bash`           | Pointer to another file  |
| `p`    | Named pipe (FIFO) | `/tmp/myfifo`              | IPC mechanism            |
| `s`    | Socket            | `/run/docker.sock`         | Network IPC              |

---

### 🔹 Special Virtual File Systems

| Path    | Purpose                         |
| ------- | ------------------------------- |
| `/proc` | Process & kernel info (runtime) |
| `/sys`  | Hardware & driver interface     |
| `/dev`  | Device files                    |

Example:

```bash
cat /proc/meminfo
```

➡️ Reads **live kernel memory data** like a file.

---

## 3️⃣ What Metadata Every Linux File Has

Every file is represented internally by an **inode**.

### 🔹 View metadata

```bash
stat filename
```

---

### 📦 Core File Metadata (inode fields)

| Metadata           | Meaning                   | Why it matters           |
| ------------------ | ------------------------- | ------------------------ |
| **Inode number**   | Unique ID                 | File identity (not name) |
| **File type**      | Regular, dir, device      | Determines behavior      |
| **Permissions**    | rwx for user/group/others | Security                 |
| **Owner (UID)**    | File owner                | Access control           |
| **Group (GID)**    | Group ownership           | Shared access            |
| **Size**           | File size in bytes        | Storage                  |
| **Link count**     | Hard links                | Deletion logic           |
| **Timestamps**     | Time tracking             | Auditing                 |
| **Block pointers** | Disk location             | Data access              |

---

### ⏱️ Linux File Timestamps (Very Important)

| Timestamp | Meaning     | Updates when     |
| --------- | ----------- | ---------------- |
| **atime** | Access time | File read        |
| **mtime** | Modify time | Content changed  |
| **ctime** | Change time | Metadata changed |

Example:

```bash
chmod 644 file.txt   # updates ctime, not mtime
```

---

### 🔗 Hard Link Insight

- Multiple filenames → same inode
- Data deleted only when **link count = 0**

```bash
ln a.txt b.txt
```

---

## 4️⃣ Important Linux Commands (Files & Filesystem)

---

### 📁 File & Directory Navigation

```bash
ls        # list files
ls -l     # detailed view
ls -a     # show hidden files
pwd       # current directory
cd        # change directory
tree      # directory tree
```

---

### 📄 File Operations

```bash
touch file.txt
cp a b
mv a b
rm file
rm -r dir
cat file
less file
head file
tail file
```

---

### 🔐 Permissions & Ownership

```bash
chmod 755 file
chmod u+x file
chown user file
chgrp group file
```

---

### 🔍 File Inspection

```bash
stat file
file binary
inode=$(ls -i file)
```

---

### 💾 Filesystem & Disk

```bash
df -h        # disk usage
du -sh dir   # directory size
mount
umount
lsblk
blkid
```

---

### 🔎 Search & Analysis

```bash
find / -name "*.log"
locate passwd
grep "error" file
```

---

### 🔧 Device & Special Files

```bash
ls /dev
cat /dev/null
echo "hi" > /dev/tty
```

---

## 5️⃣ Mental Model (Interview-Ready)

> **Linux treats everything as a file to achieve simplicity, composability, and power.
> By exposing all resources through the filesystem abstraction, Linux enables uniform access, strong security, and unmatched flexibility.**

---

## 📁 All Linux File Types — **Deep, System-Level Explanation**

Linux does **not** see files the way humans do (text, pdf, image).
Internally, Linux classifies files by **behavior**, not by extension.

---

## 1️⃣ Regular (Ordinary) File `-`

### 🔹 What it is

A **stream of bytes stored on disk**.
Linux does not care whether it is text, image, or executable.

### 🔹 Examples

```text
/etc/passwd
notes.txt
main.c
a.out
```

### 🔹 Sub-types (by convention)

| Type        | How Linux identifies        |
| ----------- | --------------------------- |
| Text file   | ASCII / UTF-8               |
| Binary file | Non-text bytes              |
| Executable  | `x` permission + ELF header |
| Object file | `.o`                        |

Check type:

```bash
file a.out
```

### 🔹 Key properties

- Stored on disk
- Has inode & data blocks
- Read/write sequentially or randomly

### 🔹 Kernel view

```text
inode → data blocks
```

---

## 2️⃣ Directory File `d`

### 🔹 What it is

A **mapping table**:

```text
filename → inode number
```

### 🔹 Example

```bash
/home/arj
/etc
```

### 🔹 Important facts

- Directory **does NOT store file data**
- It stores **names + inode numbers**
- Kernel resolves paths recursively

### 🔹 Permissions meaning

| Permission | Meaning                |
| ---------- | ---------------------- |
| `r`        | List files (`ls`)      |
| `w`        | Create/delete files    |
| `x`        | Enter directory (`cd`) |

```bash
ls -ld /etc
```

---

## 3️⃣ Character Device File `c`

### 🔹 What it is

A **byte-stream device** that handles data **character by character**.

### 🔹 Examples

```bash
/dev/tty
/dev/null
/dev/random
```

### 🔹 Behavior

- No buffering by kernel
- Sequential access only
- Usually user-interactive devices

### 🔹 Real use

```bash
echo "hello" > /dev/tty
```

➡️ Writes directly to terminal.

---

## 4️⃣ Block Device File `b`

### 🔹 What it is

Devices that transfer data in **blocks (chunks)**.

### 🔹 Examples

```bash
/dev/sda
/dev/nvme0n1
```

### 🔹 Characteristics

| Feature       | Block Device |
| ------------- | ------------ |
| Buffered      | ✅           |
| Random access | ✅           |
| Mountable     | ✅           |

### 🔹 Used for

- Hard disks
- SSDs
- USB drives

```bash
lsblk
```

---

## 5️⃣ Symbolic Link `l`

### 🔹 What it is

A **file containing a path to another file**.

### 🔹 Example

```bash
/bin/sh → bash
```

### 🔹 Create

```bash
ln -s target linkname
```

### 🔹 Properties

| Feature                  | Symlink |
| ------------------------ | ------- |
| Has own inode            | ✅      |
| Can cross filesystem     | ✅      |
| Breaks if target deleted | ❌      |

---

## 6️⃣ Hard Link (Special case of regular file)

_(Same type as regular file, but behavior differs)_

### 🔹 What it is

Another **directory entry** pointing to the **same inode**.

```bash
ln file1 file2
```

### 🔹 Key insight

- No “original” file
- File exists until **link count = 0**

```bash
ls -li
```

---

## 7️⃣ Named Pipe (FIFO) `p`

### 🔹 What it is

A **persistent IPC channel**.

### 🔹 Create

```bash
mkfifo mypipe
```

### 🔹 Behavior

- One process writes
- Another reads
- Blocks until both exist

### 🔹 Use case

```bash
producer > mypipe
consumer < mypipe
```

---

## 8️⃣ Socket File `s`

### 🔹 What it is

Endpoint for **inter-process communication** (IPC).

### 🔹 Examples

```bash
/run/docker.sock
/var/run/dbus/system_bus_socket
```

### 🔹 Characteristics

| Feature          | Socket |
| ---------------- | ------ |
| Bi-directional   | ✅     |
| Network or local | ✅     |
| Kernel managed   | ✅     |

---

## 9️⃣ Virtual / Pseudo Files

## 🔹 What they are

Files that **don’t exist on disk**.

### 🔹 Examples

```bash
/proc/cpuinfo
/proc/meminfo
/sys/class/net
```

### 🔹 Purpose

- Kernel → user communication
- Runtime system info
- Hardware control

```bash
cat /proc/uptime
```

---

## 1️⃣0️⃣ Executable Files (Permission-Based)

### 🔹 What defines executable?

```bash
-rwxr-xr-x
```

### 🔹 Kernel flow

1. Checks execute permission
2. Reads ELF header
3. Loads into memory
4. Starts process

```bash
./program
```

---

## 🔥 Master Mental Model

```
Everything in Linux is a file
↓
Every file has an inode
↓
Inode defines behavior
↓
Kernel dispatches to driver or FS
```

---

## 🎯 Interview Gold Lines

> “Linux file types are defined by how the kernel interacts with them, not by extensions.”

> “Directories are files mapping names to inode numbers.”

> “Devices are accessed using file I/O calls.”

---

# Linux File System — Detailed and Structured Explanation

## 1. What is the Linux File System?

The Linux file system is a **single hierarchical directory tree** that starts at the **root directory `/`**.
All files, devices, processes, configurations, and external storage are **mounted somewhere under `/`**.

Key principles:

- Single root (`/`)
- Everything is accessed via paths
- Filesystem follows **Filesystem Hierarchy Standard (FHS)**
- Supports multiple physical disks unified into one tree

---

## 2. Root Directory `/`

`/` is the top-level directory.
It contains only **critical system directories**, not user files.

If `/` is corrupted or unavailable:

- System cannot boot
- Kernel cannot start user space

---

## 3. Root-Level Directories and Their Meaning

### `/bin` — Essential User Binaries

Contains **core command-line utilities** required for:

- Booting
- Recovery mode
- Single-user mode

Examples:

- `ls`
- `cp`
- `mv`
- `rm`
- `bash`

Important notes:

- Required even when `/usr` is not mounted
- Used by all users
- In modern systems, often merged with `/usr/bin`

---

### `/sbin` — System Binaries

Contains **administrative commands** used for system control.

Examples:

- `mount`
- `fsck`
- `reboot`
- `ip`

Important notes:

- Primarily for root
- Not intended for regular users
- Often merged into `/usr/sbin`

---

### `/boot` — Boot Components

Contains files needed **before the kernel hands control to user space**.

Includes:

- Kernel image (`vmlinuz`)
- Initramfs
- Bootloader configuration (GRUB)

Developer note:

- Never modify manually unless working on boot/kernel

---

### `/dev` — Device Files

Contains **device nodes** that act as interfaces to hardware.

Types:

- Character devices (keyboard, terminal)
- Block devices (disks, SSDs)

Examples:

- `/dev/sda`
- `/dev/null`
- `/dev/tty`

Key facts:

- Files are created dynamically
- Not stored on disk
- Used by kernel drivers

---

### `/etc` — System Configuration

Contains **system-wide configuration files**.

Examples:

- `/etc/passwd`
- `/etc/hosts`
- `/etc/ssh/sshd_config`

Rules:

- Text files only
- No binaries
- No user data

Developer best practice:

- Application configuration belongs here

---

### `/home` — User Home Directories

Contains personal directories for users.

Structure:

- `/home/username`

Includes:

- Documents
- Downloads
- Shell configs (`.bashrc`)
- App configs

Important:

- User-specific data only
- Permissions isolate users

---

### `/lib` and `/lib64` — Shared Libraries

Contains **critical shared libraries** required by binaries in `/bin` and `/sbin`.

Examples:

- `libc.so`
- Dynamic loader (`ld-linux.so`)

Notes:

- Needed during boot
- Deleting or breaking these makes system unusable

---

### `/usr` — Userland Software

Despite the name, `/usr` is **not user-specific**.

Structure:

- `/usr/bin` → most user commands
- `/usr/lib` → libraries
- `/usr/share` → architecture-independent data

Key insight:

- Majority of installed software lives here
- Safe to mount read-only in stable systems

---

### `/var` — Variable Data

Contains files that **change frequently**.

Subdirectories:

- `/var/log` → logs
- `/var/cache` → caches
- `/var/lib` → application state
- `/var/spool` → mail, print jobs

Developer rule:

- Logs must go here
- Databases often store data here

---

### `/tmp` — Temporary Files

Used for short-lived files.

Characteristics:

- World-writable
- Cleared on reboot or periodically

Rules:

- Never store persistent data
- Applications must handle deletion

---

### `/proc` — Process and Kernel Information

A **virtual filesystem** generated by the kernel.

Contains:

- Process directories (`/proc/PID`)
- System info (`/proc/cpuinfo`, `/proc/meminfo`)

Key properties:

- Files do not exist on disk
- Reading triggers kernel code
- Writing may change kernel behavior

---

### `/sys` — Kernel and Hardware Interface

Another virtual filesystem.

Purpose:

- Exposes kernel objects
- Controls devices and drivers

Examples:

- `/sys/class/net`
- `/sys/devices`

Used for:

- Hardware introspection
- Power management
- Driver configuration

---

### `/run` — Runtime State

Stores **volatile runtime data**.

Includes:

- PID files
- Unix sockets
- Lock files

Important:

- Exists only during system runtime
- Cleared on reboot

---

### `/opt` — Optional / Third-Party Software

Used for software not managed by system package manager.

Examples:

- `/opt/google`
- `/opt/oracle`

Use case:

- Vendor-provided binaries
- Self-contained applications

---

### `/mnt` and `/media` — Mount Points

Used to attach external filesystems.

- `/mnt` → temporary/manual mounts
- `/media` → auto-mounted devices (USB, SD cards)

---

## 4. How the Linux File System Works Internally

Conceptual flow:

- Disk contains filesystem (ext4, xfs, etc.)
- Filesystem stores inodes
- Directories map names to inode numbers
- Kernel uses VFS to abstract filesystem types

System calls:

- `open()`
- `read()`
- `write()`
- `close()`

These calls work identically for:

- Regular files
- Devices
- Pipes
- Sockets
- Virtual files

---

## 5. Important Points for Developers

### 1. Respect Directory Semantics

Do not place:

- Logs in `/etc`
- Configs in `/var`
- Binaries in `/home`

---

### 2. Do Not Hardcode Paths

Use:

- `$PATH`
- `/usr/bin/env`

Avoid:

- `/bin/bash` hardcoding

---

### 3. Permissions and Ownership Matter

Always consider:

- UID
- GID
- `umask`

---

### 4. Virtual Files Behave Differently

Files under `/proc` and `/sys`:

- Cannot seek
- Generated dynamically
- May change on every read

---

### 5. Mounting Changes Reality

A mount can:

- Hide existing directories
- Replace contents dynamically

---

## 6. Interview-Ready Summary

Linux uses a single-rooted hierarchical filesystem defined by the Filesystem Hierarchy Standard.
Each top-level directory has a strict semantic purpose, enabling clarity, security, and maintainability.
The kernel exposes all resources through the filesystem using the VFS abstraction, allowing uniform access via standard system calls.

---

## 1. `cd` — Change Directory

The `cd` command is used to **change the current working directory** in the shell.

### Syntax

```bash
cd [OPTION] [DIRECTORY]
```

### Behavior

- Without arguments: `cd` → goes to the **user’s home directory**
- `cd -` → switches to **previous working directory**
- `cd ~username` → goes to **another user’s home directory**
- Supports **absolute paths** (`/home/arj`) and **relative paths** (`../dir`)

---

### Common Options

| Option | Function                                             |
| ------ | ---------------------------------------------------- |
| `-`    | Switch to previous directory (`OLDPWD`)              |
| `~`    | Home directory shortcut                              |
| `..`   | Parent directory                                     |
| `.`    | Current directory (usually used in scripts)          |
| `-P`   | Resolve **physical path** (follow symlinks)          |
| `-L`   | Follow **logical path** (default, respects symlinks) |

### Examples

```bash
cd /etc         # Absolute path
cd ../var        # Move to parent and then var
cd ~            # Go to home
cd -            # Switch to previous directory
cd -P /tmp      # Follow physical path, ignoring symlinks
```

### Notes for Developers

- `cd` is a **shell built-in**, not a binary.
  Example: `type cd` → `cd is a shell builtin`
- Useful in **scripts** to change working context
- `PWD` and `OLDPWD` environment variables store current and previous directories

---

## 2. `ps` — Process Status

The `ps` command **displays information about currently running processes**.

### Syntax

```bash
ps [options]
```

### Common Options

| Option        | Function                                                  |
| ------------- | --------------------------------------------------------- |
| `-e` or `-A`  | Show all processes                                        |
| `-f`          | Full-format listing (UID, PID, PPID, start time, command) |
| `-u <user>`   | Show processes of a specific user                         |
| `-x`          | Include processes **without controlling terminal**        |
| `-o <format>` | Customize output fields                                   |
| `-p <pid>`    | Show info for specific process ID                         |
| `-l`          | Long format with more details                             |
| `--forest`    | Show processes in **tree structure**                      |

### Important Fields in Output

| Field         | Meaning                             |
| ------------- | ----------------------------------- |
| PID           | Process ID                          |
| PPID          | Parent process ID                   |
| UID           | User ID of process owner            |
| CMD / COMMAND | Command that started the process    |
| STAT          | Process state (`R`, `S`, `Z`, etc.) |
| %CPU          | CPU usage                           |
| %MEM          | Memory usage                        |
| TTY           | Terminal associated with process    |
| START         | Process start time                  |

### Examples

```bash
ps            # Processes in current terminal
ps -ef        # All processes in full format
ps -u arj     # Processes for user 'arj'
ps -p 1234    # Info about PID 1234
ps aux        # Another common syntax: all processes with user, memory, CPU
ps --forest   # Show process hierarchy tree
```

### Notes for Developers

- `ps` shows a **snapshot** at the time of execution (use `top` or `htop` for dynamic monitoring)
- Fields can be **customized** using `-o`:

```bash
ps -eo pid,ppid,cmd,%mem,%cpu
```

- Useful in **scripts** to check if processes are running or to kill specific processes

---

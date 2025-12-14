# <span style="color:#a2d2ff">**Lesson-4:Basic Linux Commands**</span>

## <span style="color:#ffb703">**whoami**</span>

### 🧠 **Definition**

**`whoami`** stands for **“Who Am I?”**
It prints the **effective username** of the current user.

```bash
$ whoami
ec2-user
```

This tells you: "I’m currently acting as `ec2-user`."

---

### ✅ **Use Cases of `whoami`**

| Use Case                        | Description                                                           |
| ------------------------------- | --------------------------------------------------------------------- |
| ✅ **Check current user**       | Useful when switching users with `sudo su`, `su`, or SSH              |
| ✅ **Debug permissions issues** | Knowing which user is running can help fix "permission denied" errors |
| ✅ **Scripting and logging**    | Automatically log or act based on the current user                    |
| ✅ **Verify user after login**  | Especially when using automation tools or SSH key-based access        |

---

### ⚙️ **How `whoami` works internally**

It returns the **effective user ID** (`EUID`) of the process running the shell.

Technically, it's equivalent to:

```bash
id -un
```

Where:

- `id` → user identity
- `-u` → return user ID
- `-n` → return name instead of numeric ID

---

### 📦 `whoami` vs Similar Commands

| Command    | What it does                                                   |
| ---------- | -------------------------------------------------------------- |
| `whoami`   | Shows the **current user name**                                |
| `who am i` | Shows the **user logged into the terminal**                    |
| `id`       | Shows UID, GID, and all groups                                 |
| `logname`  | Shows the name of the **original login user**                  |
| `users`    | Shows **all users currently logged in**                        |
| `who`      | Shows detailed session info (like `who am i`, but system-wide) |

---

### 🔍 Example Scenario

```bash
$ whoami
ubuntu

$ sudo su -
# whoami
root
```

Here, `whoami` reflects the **current shell's effective user** — first it's `ubuntu`, then `root`.

---

### 🧰 Common Usage in Scripts

```bash
#!/bin/bash
if [ "$(whoami)" != "root" ]; then
  echo "You must run this script as root"
  exit 1
fi
```

✅ This ensures only the root user can run the script.

---

### 🔧 Flags/Options?

- `whoami` has **no options or flags** — it's a very minimal utility.
- For detailed user info, use:

```bash
id        # Full identity (UID, GID, groups)
id -u     # User ID
id -un    # Same as whoami
```

---

### ✅ Summary

| Feature       | Description                 |
| ------------- | --------------------------- |
| Command       | `whoami`                    |
| Output        | Effective username          |
| Use           | Identity check, scripting   |
| Equivalent to | `id -un`                    |
| No flags      | Very lightweight and simple |

---

![whoami](img/whoami.png)

## <span style="color:#ffb703">**ls command**</span>

### What is `ls`?

The `ls` command is used to **list files and directories** in a directory. It is one of the most commonly used commands in Unix/Linux.

---

### Viewing Help and Manual

- `man ls` → Opens manual documentation for `ls`.
- `ls --help` → Lists all available options with brief descriptions.

---

### Common Variants of `ls`

### 1) `ls`

- Lists all files and directories in alphabetical order.

### 2) `ls -r`

- Lists all files in **reverse alphabetical order**.

### 3) `ls | more`

- Displays output **line by line**.
- Press `q` to quit.

### 4) `ls | pg`

- Displays output **page by page** (20 lines per page).
- Press `q` to quit.

### 5) `ls -l`

- Long listing format showing detailed info like permissions, owner, size, etc.

### 6) `ls -t`

- Sort by **last modified time**, most recent files first.

### 7) `ls -rt`

- Sort by **last modified time**, but in **reverse order** (oldest first).

### 8) `ls -a`

- Show **all files**, including hidden files (starting with `.`), including `.` and `..`.

### 9) `ls -A`

- Show all hidden files **except** `.` and `..`.

### 10) `ls -F`

- Display **file types**:

  - `/` → directory
  - `*` → executable
  - `@` → symbolic link

### 11) `ls -f`

- Disable sorting and color formatting.

### 12) `ls -i`

- Show **inode numbers** (file system index numbers).
- Inode contains attributes like size, owner, creation time, etc.

### 13) `ls -R`

- Recursive listing: includes contents of subdirectories.

### 14) `ls -s`

- Show file size in **blocks**.
- In Ubuntu, 1 block = 1 KB.

### 15) `ls -h`

- **Human-readable** sizes (e.g., 2K, 5M).

### 16) `ls -S`

- Sort files by **size**, largest first.

### 17) `ls -rS`

- Sort by **size**, smallest first.

### 18) `ls -lS`

- Long listing with size-based sorting.

### 19) `ls -lh`

- Long listing + human-readable sizes.

### 20) `ls -alh`

- All files (including hidden), long listing, human-readable.

### 21) `ls --color=auto`

- Enable colorized output (usually default).

### 22) `ls --group-directories-first`

- List **directories first**, then files.

### 23) `ls -1`

- Display **one entry per line**.

### 24) `ls -p`

- Add `/` to directory names to distinguish them.

### 25) `ls -n`

- Long listing but shows **UID and GID numbers** instead of names.

### 26) `ls --time=atime` / `--time=access`

- Sort by **last access time** instead of modified time.

### 27) `ls --time=ctime`

- Sort by **change time** (like permission change).

### 28) `ls -v`

- Sort by **version** number (e.g., file1, file2, file10).

### 29) `ls -X`

- Sort files by **extension**.

### 30) `ls --full-time`

- Long listing with **full timestamps** (includes seconds and time zone).

### 31) `ls -c`

- Sort by **change time** (metadata change).

### 32) `ls -u`

- Sort by **last access time**.

---

### Commonly Used Combinations

- `ls -alh` → All files + long format + human-readable.
- `ls -lS` → Sort by size.
- `ls -lt` → Sort by time (most recent first).
- `ls -lrt` → Sort by time (oldest first).
- `ls -lh --group-directories-first` → Friendly view for users.

---

### Summary Table

| Option                      | Meaning                         |
| --------------------------- | ------------------------------- |
| `-a`                        | All files including hidden      |
| `-A`                        | Almost all (excluding . and ..) |
| `-l`                        | Long listing                    |
| `-h`                        | Human-readable sizes            |
| `-t`                        | Sort by modification time       |
| `-S`                        | Sort by size                    |
| `-r`                        | Reverse order                   |
| `-R`                        | Recursive listing               |
| `-F`                        | Show file types                 |
| `-i`                        | Show inode number               |
| `-1`                        | One entry per line              |
| `-p`                        | Add `/` to folders              |
| `--color=auto`              | Enable colors                   |
| `--group-directories-first` | Group folders first             |

---

### Pro Tip

To make `ls -alh --color=auto` the default behavior, you can alias it:

```bash
alias ls='ls -alh --color=auto'
```

Add this line to your `.bashrc` or `.zshrc`.

---

## <span style="color:#ffb703">**What is an Inode Number in Linux?**</span>

An **inode (index node)** is a **data structure** in a Unix/Linux file system that stores all the **metadata about a file or directory**—except its name and actual data.

---

### 🧠 Think of it Like:

A **library catalog card** that tells you everything about a book—author, publisher, year—**but not the book’s content** or the title printed on the spine.

---

### 📦 What Information Does an Inode Contain?

Each file or directory has a unique inode that stores:

| Attribute           | Description                                        |
| ------------------- | -------------------------------------------------- |
| File type           | Regular file, directory, symbolic link, etc.       |
| Permissions         | Read/write/execute bits for owner, group, others   |
| Owner info          | User ID (UID) and Group ID (GID)                   |
| File size           | In bytes                                           |
| Timestamps          | Last access, last modified, inode change time      |
| Link count          | Number of hard links to the file                   |
| Data block pointers | Addresses of the disk blocks where file data lives |

---

### 🔢 What is an Inode Number?

- It is simply the **ID** (an integer) assigned to each inode.
- When you run `ls -i`, it shows the **inode number** of each file:

```bash
$ ls -i
1933027  myfile.txt
```

This means `myfile.txt` is associated with inode number `1933027`.

---

### 📂 Where is File Name Stored Then?

- File names are stored in **directory files**, which map **file names to inode numbers**.
- This is why **you can have multiple file names (hard links)** pointing to the same inode.

---

### 🛠️ Use Cases of Inodes

1. **Hard Links**: Multiple filenames pointing to the same inode.
2. **Finding Duplicates**: Same inode → Same file.
3. **Deleted but Open Files**: File removed from directory, but data stays until all inodes are freed.
4. **Debugging file system issues** with `df`, `du`, `fsck`.

---

### 🔎 Check Inode of a File

```bash
ls -i filename.txt
```

### 🧮 Check File System Inode Usage

```bash
df -i
```

Shows inode usage like disk space.

---

## <span style="color:#ffb703">**🕒 Linux `date` Command — Detailed Notes**</span>

The `date` command in Linux is used to **display and set the system date and time**.

### 📌 Basic Syntax

```bash
date [OPTION]...
```

---

### 📆 Common Use Cases

| Use Case                     | Command                     |
| ---------------------------- | --------------------------- |
| Show current date and time   | `date`                      |
| Display only date            | `date +%D` → `mm/dd/yy`     |
| Display only time            | `date +%T` → `hh:mm:ss`     |
| Schedule scripts with `cron` | Used in logs or time stamps |
| Format output for scripts    | `date +%Y-%m-%d_%H-%M-%S`   |

---

### 🔠 Format Specifiers

You can customize the output of the `date` command using **format specifiers**, prefixed with `%`.

| Format | Description                      | Example      |
| ------ | -------------------------------- | ------------ |
| `%D`   | Date in mm/dd/yy                 | `07/19/25`   |
| `%T`   | Time in hh\:mm\:ss               | `16:08:45`   |
| `%d`   | Day of the month (01..31)        | `19`         |
| `%m`   | Month (01..12)                   | `07`         |
| `%y`   | Last two digits of year (00..99) | `25`         |
| `%Y`   | Full year (e.g., 2025)           | `2025`       |
| `%H`   | Hour in 24-hour format (00..23)  | `16`         |
| `%I`   | Hour in 12-hour format (01..12)  | `04`         |
| `%M`   | Minute (00..59)                  | `08`         |
| `%S`   | Second (00..59)                  | `45`         |
| `%A`   | Full weekday name                | `Saturday`   |
| `%a`   | Short weekday name               | `Sat`        |
| `%B`   | Full month name                  | `July`       |
| `%b`   | Short month name                 | `Jul`        |
| `%Z`   | Timezone abbreviation            | `IST`        |
| `%z`   | Numeric timezone offset          | `+0530`      |
| `%j`   | Day of year (001..366)           | `201`        |
| `%u`   | Day of week (1 = Monday)         | `6`          |
| `%w`   | Day of week (0 = Sunday)         | `6`          |
| `%s`   | Seconds since epoch              | `1721386725` |
| `%N`   | Nanoseconds (may be zero-padded) | `000000000`  |

---

### 🧪 Examples

### 1. Print full date and time:

```bash
date
```

📤 Output:

```
Sat Jul 19 16:08:45 IST 2025
```

### 2. Print formatted timestamp for a file:

```bash
date +%Y-%m-%d_%H-%M-%S
```

✅ Useful for backups/logs like `backup_2025-07-19_16-08-45.log`

### 3. Get current weekday:

```bash
date +%A
```

### 4. Display ISO-8601 format:

```bash
date --iso-8601
```

📤 Output: `2025-07-19`

---

### 🛠️ Advanced Options

### 🔁 Set System Date and Time (requires sudo)

```bash
sudo date MMDDhhmm[[CC]YY][.ss]
```

🔍 Example:

```bash
sudo date 071916082025.30
```

→ Sets date to July 19, 2025, 16:08:30

### 🌐 Set Hardware Clock from System Clock

```bash
sudo hwclock --systohc
```

### 🧾 View UTC Time

```bash
date -u
```

### 📚 Manual and Help

```bash
man date
-- or --
date --help
```

---

### 🔚 Summary

- `date` is used for viewing and manipulating date/time.
- Most useful when scripting, logging, or formatting human-readable timestamps.
- Supports **dozens of format options** using `%` symbols.

---

## <span style="color:#ffb703">**📅 Linux `cal` Command — Calendar Viewer**</span>

The `cal` command is used to **display a calendar** in the terminal.

### 📌 Basic Syntax

```bash
cal [month] [year]
```

### 📆 Examples and Use Cases

| Command       | Output Description                       |
| ------------- | ---------------------------------------- |
| `cal`         | Current month calendar                   |
| `cal 2020`    | Full calendar of the year 2020           |
| `cal 08 2019` | August 2019 calendar                     |
| `cal 1`       | Calendar for January of current year     |
| `cal 9999`    | Calendar for the year 9999 (max allowed) |
| `cal 10000`   | ❌ Error: year not in range 1..9999      |

📝 **Note**: `cal` supports years only from `1` to `9999`. Trying beyond that will result in an error.

---

### 🔄 Useful Options

| Option     | Description                            |
| ---------- | -------------------------------------- |
| `-y`       | Print entire current year              |
| `-3`       | Show previous, current, and next month |
| `-m MONTH` | Show calendar for a specific month     |
| `-A N`     | Show N months after the current month  |
| `-B N`     | Show N months before the current month |

### Example with Options:

```bash
cal -3
```

📤 Output: Shows last, current, and next month's calendars side by side.

---

### 📚 Manual and Help

```bash
man cal
-- or --
cal --help
```

---

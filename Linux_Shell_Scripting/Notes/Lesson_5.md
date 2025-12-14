# <span style="color:#a2d2ff">**Lesson-5:Working with Directories**</span>

## <span style="color:#ffb703">**📁 Linux `mkdir` Command — Make Directory**</span>

The `mkdir` (make directory) command is used to **create new directories** in Linux.

---

### 📌 Basic Syntax

```bash
mkdir [OPTION]... DIRECTORY...
```

---

### 🔧 Common Use Cases

| Command                   | Description                                                                  |
| ------------------------- | ---------------------------------------------------------------------------- |
| `mkdir dir1`              | Create a single directory named `dir1`                                       |
| `mkdir dir1 dir2 dir3`    | Create multiple directories at once                                          |
| `mkdir dir1/dir2/dir3`    | ❌ Fails if intermediate directories (`dir1/dir2`) don’t exist               |
| `mkdir -p dir1/dir2/dir3` | ✅ Creates full directory path, even if intermediate directories don’t exist |

---

### 🛠️ Options with Description

| Option        | Description                                                                 |
| ------------- | --------------------------------------------------------------------------- |
| `-p`          | Create parent directories as needed. No error if directory exists.          |
| `-v`          | Verbose mode. Prints each directory as it's created.                        |
| `--mode=MODE` | Set file mode (permissions) of created directories using symbolic or octal. |
| `--help`      | Display help documentation.                                                 |
| `--version`   | Display version info of `mkdir`.                                            |

---

### 🔑 Examples

### 1. Create a single directory:

```bash
mkdir my_folder
```

### 2. Create multiple directories:

```bash
mkdir dir1 dir2 dir3
```

### 3. Create nested directories (will fail if parents don’t exist):

```bash
mkdir a/b/c  # ❌ Error if `a` or `a/b` doesn't exist
```

### 4. Create nested directories with `-p`:

```bash
mkdir -p a/b/c  # ✅ Creates all necessary parent directories
```

### 5. Create directory and see output (verbose):

```bash
mkdir -vp folder1/folder2
```

📤 Output:

```
mkdir: created directory 'folder1'
mkdir: created directory 'folder1/folder2'
```

### 6. Create directory with custom permissions (e.g., 755):

```bash
mkdir --mode=755 secure_folder
```

📝 Tip: Use `ls -ld foldername` to check directory permissions.

---

### 📚 Manual and Help

```bash
man mkdir
mkdir --help
```

---

### 📌 Summary

- Use `mkdir` to create directories.
- `-p` is essential for nested paths.
- Combine `-v` with `-p` for feedback.
- Use `--mode` to set permissions during creation.

---

## <span style="color:#ffb703">**`rmdir` Command — Remove Empty Directories**</span>

### 📌 Syntax

```bash
rmdir [OPTION]... DIRECTORY...
```

### ✅ Use Cases

| Command           | Description                        |
| ----------------- | ---------------------------------- |
| `rmdir dir1`      | Removes the empty directory `dir1` |
| `rmdir dir1/dir2` | Removes `dir2` if it's empty       |

### ⚠️ Limitations of `rmdir`

- ❌ **Can only delete empty directories**.
- ❌ Cannot delete a directory containing **files** or **subdirectories**.
- ❌ Cannot recursively delete directories.
- ❌ No prompt or confirmation — silently fails if not empty.

### Example:

```bash
mkdir -p test/empty
rmdir test/empty   # ✅ Success
rmdir test         # ✅ Success (if empty after removing above)
```

---

## <span style="color:#ffb703">**`rm` Command — Remove Files or Directories**</span>

### 📌 Syntax

```bash
rm [OPTION]... FILE...
```

### ✅ Use Cases

| Command          | Description                                     |
| ---------------- | ----------------------------------------------- |
| `rm file.txt`    | Deletes a single file                           |
| `rm -i file.txt` | Prompts before deletion                         |
| `rm *.txt`       | Deletes all `.txt` files in current directory   |
| `rm -r folder`   | Deletes folder and all its contents recursively |
| `rm -rf folder`  | Forcefully deletes folder without prompt        |
| `rm -v file.txt` | Verbosely shows what is being deleted           |

### 🛠️ Common `rm` Options

| Option                | Description                                                      |
| --------------------- | ---------------------------------------------------------------- |
| `-r` or `--recursive` | Recursively delete directories and contents                      |
| `-f` or `--force`     | Ignore nonexistent files and suppress prompts                    |
| `-i`                  | Prompt before every removal                                      |
| `-I`                  | Prompt once before removing more than three files or recursively |
| `-v`                  | Show what’s being deleted (verbose mode)                         |
| `--no-preserve-root`  | Allow recursive delete of `/` (dangerous!)                       |
| `--preserve-root`     | Default: avoid removing `/`                                      |

### 🛑 Why Use `rm` Carefully?

- `rm` **permanently deletes files** — no "trash bin" or recovery.
- `rm -rf /` can **wipe the entire system** if used incorrectly.
- No confirmation unless `-i` is used.
- Dangerous in scripts — use conditional checks before running.

### 🔐 Safe Practices

- Use `-i` or `-I` for prompts:

  ```bash
  rm -i important_file.txt
  ```

- Use `ls` first to verify:

  ```bash
  ls *.log
  rm *.log
  ```

- Test with `echo` before actual execution:

  ```bash
  echo rm *.tmp
  ```

### 📚 Help and Manual

```bash
man rm
man rmdir
```

### ✅ Summary

| Command | Usage                            | Best For                             |
| ------- | -------------------------------- | ------------------------------------ |
| `rmdir` | Remove empty directories         | Simple cleanup of empty folders      |
| `rm`    | Remove files or full directories | Complete deletion (use with caution) |

---

## <span style="color:#ffb703">**brace expansion**</span>

- brace expansion** `{}` — a powerful shell feature (mainly in **bash**) that allows you to **generate multiple strings from a pattern\*\*.

### 🔍 Your Command Breakdown:

```bash
mkdir {sunny,katrina,kareena}/{jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dec}_{2020,2021,2022}
```

This command will **create directories** in this structure:

#### 🧱 Folder Structure:

- For each person (`sunny`, `katrina`, `kareena`)
- Create subdirectories named like:

  - `jan_2020`, `jan_2021`, `jan_2022`, ...
  - `feb_2020`, ..., `dec_2022`

---

### 🛠️ How It Works

Brace expansion works **before** the command is executed. It expands the expression into a list of strings.

#### 🔸 `{a,b,c}` expands to:

```
a b c
```

#### 🔸 `{a,b}/{1,2}` expands to:

```
a/1 a/2 b/1 b/2
```

#### 🔸 `{jan,feb}_{2020,2021}` expands to:

```
jan_2020 jan_2021 feb_2020 feb_2021
```

So your full command expands to:

```
mkdir sunny/jan_2020 sunny/jan_2021 ... sunny/dec_2022
mkdir katrina/jan_2020 ... katrina/dec_2022
mkdir kareena/jan_2020 ... kareena/dec_2022
```

That’s a total of **3 persons × 12 months × 3 years = 108 directories!**

---

### ✅ Use Cases of Brace Expansion

| Use Case                    | Command Example                                       |
| --------------------------- | ----------------------------------------------------- |
| Create multiple files       | `touch file{1,2,3}.txt` → `file1.txt`, `file2.txt`... |
| Nested directory structures | `mkdir -p project/{src,bin,doc}`                      |
| File renaming (with `mv`)   | `mv file{1,2}.txt file{A,B}.txt`                      |
| Loops with expansion        | `for i in {1..5}; do echo $i; done`                   |

---

### ⚠️ Notes

- It’s not a loop — it’s a string generator **at shell parse time**.
- Doesn’t work inside quotes like `"{a,b}"`.
- You can use sequences too: `{1..5}`, `{a..z}`.

---

## Absolute Path vs Relative Path (Linux)

In Linux, every file and directory is identified by a **path**.
A path tells the kernel **how to locate a file in the filesystem tree**.

---

## 1. Absolute Path

### Definition

An **absolute path** is a path that:

- **Always starts from the root directory `/`**
- Is **independent of the current working directory**
- Fully specifies the location of a file or directory

### Syntax

```text
/path/from/root/to/target
```

### Examples

```bash
/home/arj/projects/app
/etc/nginx/nginx.conf
/usr/bin/gcc
```

### Key Characteristics

- Starts with `/`
- Unambiguous
- Same result regardless of where you are in the filesystem

### How the system resolves it

```text
/ → home → arj → projects → app
```

---

## 2. Relative Path

### Definition

A **relative path** is a path that:

- Is interpreted **relative to the current working directory**
- Does **not** start with `/`

### Syntax

```text
path/from/current/directory
```

### Examples

Assume current directory:

```bash
/home/arj
```

```bash
projects/app
./projects/app
../documents
```

### Special Symbols

| Symbol | Meaning           |
| ------ | ----------------- |
| `.`    | Current directory |
| `..`   | Parent directory  |

### How the system resolves it

If current directory is `/home/arj`:

```bash
cd projects
```

Kernel interprets it as:

```text
/home/arj/projects
```

---

## 3. Absolute vs Relative — Direct Comparison

| Aspect                       | Absolute Path | Relative Path     |
| ---------------------------- | ------------- | ----------------- |
| Starts with `/`              | Yes           | No                |
| Depends on current directory | No            | Yes               |
| Clarity                      | Very high     | Context-dependent |
| Portability in scripts       | High          | Risky             |
| Typing effort                | Longer        | Shorter           |

---

## 4. Using Paths for Directory Navigation

### Using Absolute Paths

```bash
cd /var/log
cd /usr/local/bin
```

Characteristics:

- Works from anywhere
- Common in scripts and system commands

---

### Using Relative Paths

```bash
cd projects
cd ../downloads
cd ./src
```

Characteristics:

- Faster to type
- Depends on current location
- Easy to break if directory changes

---

## 5. Using Paths for Directory Creation

### Absolute Path

```bash
mkdir /home/arj/work/backend
```

Creates directory regardless of current location.

---

### Relative Path

```bash
mkdir work/backend
```

Creates directories relative to current directory.

---

### Recursive Creation

```bash
mkdir -p /home/arj/work/backend/logs
mkdir -p work/backend/logs
```

---

## 6. Using Paths for File Operations

### File Creation

```bash
touch /tmp/test.txt
touch notes.txt
```

### Copying Files

```bash
cp /etc/hosts ./hosts_backup
cp src/main.c /home/arj/backup/
```

### Moving / Renaming

```bash
mv ./a.txt ../b.txt
mv /var/log/syslog /tmp/syslog.old
```

---

## 7. Using Paths in Commands and Programs

### Execution

```bash
/usr/bin/python script.py
./script.sh
```

Key difference:

- `./script.sh` → relative path
- `/home/arj/script.sh` → absolute path

---

### Configuration and Services

System services and cron jobs **must use absolute paths** because:

- No guaranteed working directory
- Environment may be minimal

Example:

```bash
* * * * * /usr/bin/python /home/arj/job.py
```

---

## 8. Paths and Environment Variables

### Home Shortcut

```bash
~
```

Expands to:

```text
/home/arj
```

Examples:

```bash
cd ~
cd ~/projects
```

---

### PATH Variable

When you run:

```bash
gcc
```

Shell searches directories listed in:

```bash
$PATH
```

This is **not a path to a file**, but a **search mechanism**.

---

## 9. Common Developer Mistakes

1. Using relative paths in scripts that run via cron or services
2. Assuming current directory in production
3. Mixing `./` and absolute paths inconsistently
4. Forgetting that `cd` affects relative path resolution

---

## 10. Developer Best Practices

- Use **absolute paths** in:

  - Scripts
  - Cron jobs
  - System services

- Use **relative paths** in:

  - Interactive shell work
  - Short-lived commands

- Always know your current directory:

```bash
pwd
```

---

## Summary

- Absolute paths start from `/` and are unambiguous
- Relative paths depend on the current working directory
- Both resolve to the same inode, but through different resolution logic
- Correct path usage is critical for reliability in scripts and production systems

---

# `cp` Command in Linux (Copy)

## 1. What is `cp`?

`cp` is used to **copy files and directories** from one location to another.

Key properties:

- Copies **data**, not inode (new file is created)
- Preserves content, but **metadata is not preserved unless explicitly requested**
- Overwrites destination **silently by default**

---

## 2. Basic Syntax

```bash
cp [OPTIONS] SOURCE DESTINATION
cp [OPTIONS] SOURCE... DIRECTORY
```

---

## 3. File → File Copy

### Command

```bash
cp source_file destination_file
```

### Behavior

- If `destination_file` does **not exist**

  - It is created

- If `destination_file` **already exists**

  - Its content is **completely overwritten**

- File permissions:

  - Destination file gets default permissions based on `umask`

### Example

```bash
cp file1 file2
```

Effect:

- `file2` becomes an exact content copy of `file1`
- Original `file2` content is lost

Important:

- No warning unless `-i` is used

---

## 4. File(s) → Directory Copy

### Command

```bash
cp file1 file2 file3 target_dir
```

### Rules

- Last argument **must be a directory**
- Directory **must already exist**
- Any number of files can be copied

### Example

```bash
cp a.txt b.txt c.txt backup/
```

Result:

```text
backup/a.txt
backup/b.txt
backup/c.txt
```

If directory does not exist:

```bash
cp: target 'backup' is not a directory
```

---

## 5. Copy All Files of One Directory to Another

### Command

```bash
cp dir1/* dir2
```

### Behavior

- Copies **only files**, not subdirectories
- `dir2` must already exist

### Example

```bash
cp logs/* archive/
```

### Important Limitation

- Does NOT copy:

  - Subdirectories
  - Hidden files (`.file`)

To include hidden files:

```bash
cp -r dir1/. dir2
```

---

## 6. Directory → Directory Copy (Recursive)

### Without `-r`

```bash
cp dir1 dir2
```

Error:

```text
cp: -r not specified; omitting directory 'dir1'
```

### Correct Command

```bash
cp -r dir1 dir2
```

---

## 7. Directory Copy — Two Important Cases

### Case 1: Destination Directory Exists

```bash
cp -r dir1 dir2
```

Result:

```text
dir2/
 └── dir1/
     ├── file1
     └── file2
```

Meaning:

- Entire `dir1` is copied **inside** `dir2`

---

### Case 2: Destination Directory Does NOT Exist

```bash
cp -r dir1 dir2
```

Result:

```text
dir2/
 ├── file1
 └── file2
```

Meaning:

- `dir2` is created
- Contents of `dir1` are copied
- `dir1` name itself is NOT preserved

This behavior is critical and often misunderstood.

---

## 8. Important `cp` Options (Must Know)

### `-r` or `-R` — Recursive

Required for directories.

```bash
cp -r src_dir dest_dir
```

---

### `-i` — Interactive (Safe Mode)

Prompts before overwrite.

```bash
cp -i file1 file2
```

Useful to prevent accidental data loss.

---

### `-f` — Force

Overwrites without asking (even read-only files).

```bash
cp -f file1 file2
```

Use with caution.

---

### `-v` — Verbose

Shows what is being copied.

```bash
cp -v file1 file2
```

---

### `-p` — Preserve Metadata

Preserves:

- Permissions
- Ownership
- Timestamps

```bash
cp -p file1 file2
```

For directories:

```bash
cp -rp dir1 dir2
```

---

### `-a` — Archive (Best Practice)

Equivalent to:

```text
-r + -p + preserve links + preserve attributes
```

```bash
cp -a dir1 dir2
```

Use when:

- Backups
- Deployments
- System file copying

---

### `-u` — Update

Copies only if source is newer.

```bash
cp -u source dest
```

Useful for incremental backups.

---

### `-n` — No Overwrite

Does not overwrite existing files.

```bash
cp -n file1 file2
```

---

## 9. Copying Symbolic Links

Default behavior:

- Copies the **target**, not the link

To copy symlink as symlink:

```bash
cp -d symlink dest
```

To follow symlinks:

```bash
cp -L symlink dest
```

---

## 10. Common Developer Use Cases

### Backup

```bash
cp -a project project_backup
```

---

### Deployment

```bash
cp -r build/* /var/www/app/
```

---

### Log Archiving

```bash
cp -u /var/log/app.log logs/
```

---

### Safe Copy

```bash
cp -iv config.conf config.conf.bak
```

---

## 11. Special Points and Pitfalls

1. `cp` **overwrites silently**
2. `cp dir/*` does not copy hidden files
3. Always use `-r` for directories
4. Use `-a` instead of `-r` for real-world copying
5. `cp` creates **new inodes**
6. Permissions change unless `-p` or `-a` is used
7. Destination behavior differs based on existence

---

## 12. Comparison with `mv`

| Aspect           | cp   | mv                    |
| ---------------- | ---- | --------------------- |
| Creates new file | Yes  | No                    |
| Original remains | Yes  | No                    |
| inode preserved  | No   | Yes (same filesystem) |
| Safer            | Less | More                  |

---

## Summary

- `cp` copies files and directories
- Recursive copy requires `-r`
- Metadata preservation requires `-p` or `-a`
- Destination existence changes behavior
- Improper usage can cause silent data loss

---

# `mv` Command in Linux (Move / Rename)

## 1. What is `mv`?

`mv` is used to **move files or directories** from one location to another, and to **rename files or directories**.

Key properties:

- Does **not create a copy**
- Operates on the **same inode** (within the same filesystem)
- Faster than `cp` because it usually only updates metadata
- Overwrites destination **silently by default**

---

## 2. Basic Syntax

```bash
mv [OPTIONS] SOURCE DESTINATION
mv [OPTIONS] SOURCE... DIRECTORY
```

---

## 3. File → File (Rename or Replace)

### Command

```bash
mv source_file destination_file
```

### Behavior

- If `destination_file` does not exist:

  - File is renamed

- If `destination_file` exists:

  - It is **overwritten**

- inode remains the same (same filesystem)

### Example

```bash
mv file1 file2
```

Effect:

- `file1` becomes `file2`
- No data copy occurs

---

## 4. File(s) → Directory

### Command

```bash
mv file1 file2 file3 target_dir
```

### Rules

- Last argument must be an existing directory
- All files are moved into the directory

### Example

```bash
mv a.txt b.txt archive/
```

Result:

```text
archive/a.txt
archive/b.txt
```

---

## 5. Directory → Directory (Move)

### Command

```bash
mv dir1 dir2
```

### Case 1: Destination directory exists

```bash
mv dir1 dir2
```

Result:

```text
dir2/
 └── dir1/
```

Meaning:

- `dir1` is moved **inside** `dir2`

---

### Case 2: Destination directory does not exist

```bash
mv dir1 dir2
```

Result:

- `dir1` is renamed to `dir2`

No recursion flag is needed.

---

## 6. Moving Across Filesystems (Important)

If source and destination are on **different filesystems**:

- `mv` internally performs:

```text
copy → delete
```

Implications:

- Slower than same-filesystem move
- inode changes
- Partial move possible if interrupted

You can detect filesystem boundaries using:

```bash
df -T
```

---

## 7. Important `mv` Options

### `-i` — Interactive

Prompts before overwrite.

```bash
mv -i file1 file2
```

Recommended for safety.

---

### `-f` — Force

Overwrites without prompt.

```bash
mv -f file1 file2
```

---

### `-n` — No Overwrite

Does not replace existing files.

```bash
mv -n file1 file2
```

---

### `-v` — Verbose

Displays what is being moved.

```bash
mv -v file1 dir/
```

---

### `-T` — Treat Destination as File

Prevents treating destination as directory.

```bash
mv -T dir1 dir2
```

Useful in scripts to avoid ambiguity.

---

### `-u` — Update

Moves only if source is newer than destination.

```bash
mv -u src dest
```

---

## 8. Renaming Use Cases (Very Common)

### Rename File

```bash
mv old.txt new.txt
```

### Rename Directory

```bash
mv old_dir new_dir
```

### Bulk Rename (with shell expansion)

```bash
mv *.txt text_files/
```

---

## 9. Metadata and Permissions

- Permissions and ownership remain unchanged
- Timestamps:

  - `ctime` changes
  - `mtime` remains same

- No new inode created (same filesystem)

---

## 10. Symlink Behavior

- Moving a symlink moves the link itself
- Target remains unchanged

```bash
mv symlink new_symlink
```

---

## 11. Common Developer Use Cases

### Reorganizing Project Structure

```bash
mv src old_src
```

---

### Log Rotation (Manual)

```bash
mv app.log app.log.1
```

---

### Safe Renaming

```bash
mv -i config.yaml config.yaml.bak
```

---

## 12. Common Mistakes and Pitfalls

1. `mv` overwrites silently without `-i`
2. Moving across filesystems causes copy + delete
3. Destination directory existence changes behavior
4. Accidentally moving into a directory instead of renaming
5. No undo mechanism

---

## 13. Comparison: `mv` vs `cp`

| Aspect              | mv            | cp     |
| ------------------- | ------------- | ------ |
| Creates new file    | No            | Yes    |
| Uses same inode     | Yes (same FS) | No     |
| Faster              | Yes           | Slower |
| Original remains    | No            | Yes    |
| Needs `-r` for dirs | No            | Yes    |

---

## 14. Summary

- `mv` moves or renames files and directories
- Fast because it usually updates metadata only
- Behavior changes based on destination existence
- Use `-i` in interactive work
- Be careful when crossing filesystem boundaries

---

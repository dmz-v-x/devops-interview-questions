### Question
How do you check the size of a directory in Linux?

### Answer

In Linux, the size of a directory can be checked using several commands. The most commonly used tool is the **`du` (Disk Usage)** command, which calculates disk usage by files and directories.

Other tools like **`ncdu`** and **`ls`** can also help analyze directory contents and file sizes.

---

### Using the `du` (Disk Usage) Command

`du` is the primary command used to check the size of directories and files.

It **recursively summarizes disk usage**, meaning it calculates the size of a directory and all files/subdirectories inside it.

Basic syntax:

```
du [options] [directory]
```

---

### Common Examples

#### Check the size of a directory

```
du /path/to/directory
```

This command displays the size of the directory and all its subdirectories.  
By default, the output is shown in **kilobytes (KB)**.

---

#### Show total size only

```
du -sh /path/to/directory
```

Options used:

- `-s` → summary (shows total size only)
- `-h` → human-readable format (KB, MB, GB)

Example:

```
du -sh /var/log
```

Output:

```
120M    /var/log
```

---

#### Show sizes of subdirectories

```
du -h --max-depth=1 /path/to/directory
```

Options used:

- `-h` → human-readable format
- `--max-depth=1` → shows the directory and its immediate subdirectories only

This command is useful when trying to determine **which subdirectory is consuming the most disk space**.

---

#### Sort directories by size

```
du -sh /path/to/directory/* | sort -h
```

This command lists all subdirectories and sorts them by size, making it easier to identify the largest ones.

---

### Using `ncdu` (NCurses Disk Usage)

`ncdu` is an **interactive disk usage analyzer** that provides an easier way to explore directory sizes.

It is not installed by default, so it may need to be installed first.

Installation:

Ubuntu / Debian:

```
sudo apt install ncdu
```

RHEL / CentOS:

```
sudo yum install ncdu
```

Run the command:

```
ncdu /path/to/directory
```

Features:

- Interactive interface
- Navigate directories easily
- Sort by size
- Quickly identify large files or folders

---

### Using `ls` (for Files Inside a Directory)

The `ls` command can display file sizes within a directory but **does not calculate directory sizes recursively**.

Example:

```
ls -lh /path/to/directory
```

Options used:

- `-l` → long listing format
- `-h` → human-readable sizes

This command is useful for viewing **individual file sizes**, but not the total directory size.

---

### Tricky Interview Questions

What is the difference between `du` and `df`?

| Command | Purpose |
|---|---|
| `du` | Shows disk usage of files and directories |
| `df` | Shows disk usage of entire filesystems |

---

How do you find which directory is consuming the most space?

```
du -h --max-depth=1 /path | sort -h
```

This displays directory sizes and sorts them so you can easily find the largest ones.

---

Why might `du` and `df` show different sizes?

- `du` counts **actual file sizes**
- `df` shows **space allocated on the filesystem**, including filesystem overhead and reserved blocks

---

How do you check directory size including hidden files?

```
du -sh /path/to/directory
```

The `du` command automatically includes **hidden files**, unlike `ls`.

---

### Interview Summary

To check the size of a directory in Linux, the most commonly used command is `du`, especially with options like `-sh` for a summarized human-readable output. Tools like `ncdu` provide an interactive way to analyze disk usage, while `ls` helps view file sizes within a directory.

### Question
What is the difference between the `df` and `du` commands in Linux?

### Answer

Both `df` and `du` are Linux commands used to check disk usage, but they measure disk space at **different levels**.

- `df` shows **disk usage at the filesystem level**.
- `du` shows **disk usage at the file or directory level**.

Understanding the difference helps when troubleshooting disk space issues.

---

### Purpose

| Command | Purpose |
|------|---------|
| `df` | Shows total, used, and available disk space for entire filesystems. |
| `du` | Shows disk space used by specific files or directories. |

---

### What They Measure

**df → Filesystem Level**

`df` reports disk usage for mounted filesystems or partitions.

Example interpretation:

- `/dev/sda1` may have **150 GB total**
- **50 GB used**
- **90 GB available**

It answers the question:

**"How full is my disk?"**

---

**du → Directory/File Level**

`du` calculates the disk usage of files and directories inside a filesystem.

It answers the question:

**"Which files or folders are using disk space?"**

---

### Example Output

#### Example using `df`

    df -h

Example output:

    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sda1       150G   50G   90G  36% /
    tmpfs            16G  1.2G   15G   8% /run

Explanation:

- `Size` → total disk size  
- `Used` → used disk space  
- `Avail` → available disk space  
- `Use%` → percentage used  
- `Mounted on` → mount point

---

#### Example using `du`

Check total size of a directory:

    du -sh /home/user/docs

Example output:

    2.3G    /home/user/docs

This shows the total disk space used by the `docs` directory.

To see sizes of subdirectories:

    du -h /home/user/docs

---

### Common Options

#### `df` options

| Option | Description |
|------|-------------|
| `-h` | Human-readable sizes (KB, MB, GB) |
| `-T` | Show filesystem type |
| `-i` | Show inode usage |

Example:

    df -hT

---

#### `du` options

| Option | Description |
|------|-------------|
| `-h` | Human-readable sizes |
| `-s` | Show total size only |
| `-a` | Include individual files |
| `--max-depth=N` | Limit directory recursion depth |

Example:

    du -h --max-depth=1 /home

---

### Key Differences

| Feature | `df` | `du` |
|------|------|------|
| Level | Filesystem level | Directory/file level |
| Measures | Total disk usage | Directory/file usage |
| Shows free space | Yes | No |
| Speed | Faster | Slower for large directories |
| Use case | Check disk capacity | Find large directories/files |

---

### Example Scenarios

Check how full the disk is:

    df -h

Find which directory is consuming space:

    du -h --max-depth=1 /

Check size of a specific directory:

    du -sh /var/log

---

### Interview Summary

`df` is used to check disk space usage at the filesystem level, showing total, used, and available space. `du` is used to measure how much space individual files or directories consume inside a filesystem.  

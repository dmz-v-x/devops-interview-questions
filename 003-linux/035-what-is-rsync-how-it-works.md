### Question  
What is `rsync` and how does it work?

---

### Answer  

---

### 1. What is rsync?

- `rsync` is a **fast, versatile file-copying and synchronization tool in Linux**  

It is used to:
- Copy files locally or between machines over a network  
- Synchronize directories efficiently by transferring only the changes (not entire files)  
- Backup data incrementally  

#### Core idea:
- It compares source and destination files and sends only differences, saving bandwidth and time  

---

### 2. Why use rsync?

- Efficient backup and synchronization  
- Saves bandwidth by transferring only changed data  
- Can preserve permissions, ownership, timestamps, and symbolic links  
- Works locally or remotely via SSH or rsync daemon  
- Reliable for large directories and incremental updates  

---

### 3. How rsync works

- Rsync uses a **delta-transfer algorithm**:

  - Compares file size and timestamps by default  
  - For changed files, breaks them into blocks  
  - Computes checksums for each block  
  - Transfers only changed blocks to destination  

- This makes it much faster than `scp` or `cp` for repeated transfers  

---

### 4. Basic rsync command syntax

```bash
rsync [options] source destination
```

- `source`: File or directory to copy  
- `destination`: Target location (local path or remote server)  

#### Remote syntax:
```bash
user@host:/path/to/destination
```

---

### 5. Common rsync options

| Option      | Description                                                           |
| ----------- | --------------------------------------------------------------------- |
| `-a`        | Archive mode (preserves permissions, ownership, symlinks, timestamps) |
| `-v`        | Verbose output                                                        |
| `-z`        | Compress data during transfer                                         |
| `-P`        | Show progress and partial transfers                                   |
| `--delete`  | Delete files at destination that no longer exist at source            |
| `-r`        | Recursive copy (for directories)                                      |
| `-h`        | Human-readable numbers                                                |
| `-e ssh`    | Use SSH for remote transfer                                           |
| `--dry-run` | Show what would happen without actually copying                       |
| `--exclude` | Exclude files or directories (supports patterns)                      |

---

### 6. Practical examples

---

#### 6.1 Local copy

```bash
rsync -av /home/user/docs/ /backup/docs/
```

- Copies all files in docs to `/backup/docs/`  
- `-a` preserves metadata  
- `-v` shows verbose output  

---

#### 6.2 Remote copy

```bash
rsync -avz /home/user/docs/ user@remote:/backup/docs/
```

- Copies files to a remote server using SSH  
- `-z` compresses files for faster transfer  

---

#### 6.3 Synchronize directories

```bash
rsync -av --delete /home/user/docs/ /backup/docs/
```

- Deletes files in destination that are removed from source  
- Keeps source and destination exactly in sync  

---

#### 6.4 Exclude files

```bash
rsync -av --exclude '*.tmp' /home/user/docs/ /backup/docs/
```

- Skips all `.tmp` files  

---

#### 6.5 Dry run

```bash
rsync -av --dry-run /home/user/docs/ /backup/docs/
```

- Simulates the operation without actually copying  

---

### 7. Rsync over network

#### Basic syntax:

```bash
rsync -avz /source/ user@remote:/destination/
```

---

#### SSH usage:

```bash
rsync -avz -e ssh /source/ user@remote:/destination/
```

---

#### Daemon mode:

- Run rsync as a service for faster large-scale transfers  

---

### 8. Troubleshooting rsync

---

#### Problem 1: Permission denied

- Cause: User doesn’t have access to source/destination  
- Solution: Use `sudo` if local, or check remote permissions  

---

#### Problem 2: Partial transfers

- Cause: Network interruption  
- Solution: Use `-P` to resume partial transfers  

---

#### Problem 3: Deleted files not removed

- Cause: `--delete` option not used  
- Solution: Add `--delete` to synchronize deletions  

---

#### Problem 4: Too many small files, slow transfer

- Solution:
  - Use compression `-z`  
  - Consider `--whole-file` if local copy  

---

#### Problem 5: Disk space issues

- Solution:
  - Check:
    ```bash
    df -h
    ```
  - Clean up destination if necessary  

---

### 9. Advantages of rsync

- Efficient: transfers only changes  
- Can resume interrupted transfers  
- Supports local and remote operations  
- Preserves metadata (permissions, timestamps)  
- Supports exclusions and selective syncing  
- Works securely over SSH  
- Handles large directories and incremental backups  

---

### 10. Common Interview Questions

---

#### Q1: Difference between `scp` and `rsync`?  
**A:**  
- `scp` copies full files every time  
- `rsync` transfers only differences and preserves metadata  

---

#### Q2: How does rsync transfer only changes?  
**A:**  
- By using checksums of file blocks and sending only modified blocks  

---

#### Q3: What does `--delete` do?  
**A:**  
- Deletes files from destination that no longer exist in source  

---

#### Q4: Can rsync resume interrupted transfers?  
**A:**  
- Yes, using `-P` or `--partial`  

---

#### Q5: How to exclude specific files from syncing?  
**A:**  
```bash
--exclude '*.log'
```

---

#### Q6: How to compress files during transfer?  
**A:**  
```bash
-z
```

---

#### Q7: Can rsync work without SSH?  
**A:**  
- Yes, via rsync daemon, but SSH is recommended for security  

---

### 11. Interview-Ready Summary

“`rsync` is a powerful file synchronization tool that efficiently transfers only changed data using a delta-transfer algorithm. It supports local and remote transfers, preserves file metadata, and is widely used for backups and syncing large datasets. Compared to traditional tools like scp, it is faster and more efficient.” :contentReference[oaicite:0]{index=0}

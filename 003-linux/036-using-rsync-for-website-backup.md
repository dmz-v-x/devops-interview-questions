### Question  
How would you use `rsync` to perform a daily website backup?

---

### Answer  

---

### 1. Example: Backup website daily

```bash
# Backup /var/www to remote server, preserve metadata, compress, and delete old files
rsync -avz --delete /var/www/ user@backup-server:/backup/www/
```

---

### 2. Explanation

- Ensures destination **mirrors source**  
- Saves bandwidth using:
  ```bash
  -z
  ```
- Preserves:
  - timestamps  
  - permissions  
  - symlinks  
  using:
  ```bash
  -a
  ```
- Deletes obsolete files at destination using:
  ```bash
  --delete
  ```

---

### 3. Summary

- `rsync` = efficient file sync and backup tool  

#### Main advantages:
- Delta-transfer (only changed data is copied)  
- Metadata preservation  
- Incremental backup  
- Remote synchronization  

---

#### Key commands:

```bash
rsync -av
rsync --delete
rsync --exclude
rsync --dry-run
rsync -P
rsync -z
rsync -e ssh
```

---

#### Troubleshooting:

- Permission issues  
- Network interruptions  
- Disk space problems  
- Slow transfer for many small files  

---

#### Use cases:

- Backup  
- Migration  
- Synchronization  
- Remote file transfers  

---

### 4. Interview-Ready Summary

“To perform a daily backup using rsync, I use a command like rsync -avz --delete to sync the source directory with a remote backup server. It preserves metadata, compresses data during transfer, and ensures the destination mirrors the source by removing outdated files. This makes it efficient for incremental backups.”

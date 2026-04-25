### Question  
Your application generates large logs in /var/log/myapp/ and there's no log rotation setup. How will you manage and automate log cleanup?

---

### Answer  

---

### 1. Problem Understanding

- Logs are continuously growing in:
  - `/var/log/myapp/`  

- Issues:
  - Disk space exhaustion  
  - Performance degradation  
  - System crashes if disk is full  

- Goal:
  - Compress old logs  
  - Delete very old logs  
  - Automate the process  

---

### 2. Solution Approach

- Create a **log cleanup script**
- Perform:
  - Compression of older logs  
  - Deletion of outdated logs  
  - Logging of cleanup actions  
- Schedule using **cron job**  

---

### 3. Log Cleanup Script

```bash
#!/bin/bash

# Directory where logs are stored
LOG_DIR="/var/log/myapp"
LOG_FILE="/var/log/myapp/log_rotation.log"

# Ensure the log directory exists
if [ ! -d "$LOG_DIR" ]; then
    echo "[$(date)] ERROR: Log directory $LOG_DIR does not exist!" >> "$LOG_FILE"
    exit 1
fi

# Compress logs older than 7 days (but newer than 30)
find "$LOG_DIR" -type f -name "*.log" -mtime +7 -mtime -30 ! -name "*.gz" \
    -exec gzip {} \; \
    -exec echo "[$(date)] Compressed: {}" >> "$LOG_FILE" \;

# Delete compressed logs older than 30 days
find "$LOG_DIR" -type f -name "*.gz" -mtime +30 \
    -exec rm -f {} \; \
    -exec echo "[$(date)] Deleted: {}" >> "$LOG_FILE" \;

# Optional: Delete uncompressed logs older than 30 days
find "$LOG_DIR" -type f -name "*.log" -mtime +30 \
    -exec rm -f {} \; \
    -exec echo "[$(date)] Deleted (uncompressed): {}" >> "$LOG_FILE" \;

# Done
echo "[$(date)] Log rotation completed successfully." >> "$LOG_FILE"
```

---

### 4. What This Script Does

- Validates log directory exists  
- Compresses:
  - Logs older than 7 days  
  - Keeps recent logs uncompressed  

- Deletes:
  - Compressed logs older than 30 days  
  - Old uncompressed logs  

- Maintains:
  - Execution log (`log_rotation.log`)  

---

### 5. Automate Using Cron

```bash
crontab -e
```

Add:

```bash
0 2 * * * /path/to/log_cleanup.sh
```

- Runs daily at **2 AM**  
- Ensures regular cleanup  

---

### 6. Best Practices

- Always:
  - Test script manually before scheduling  
  - Monitor disk usage:

```bash
df -h
```

- Use:
  - `logrotate` (production-grade alternative)  

- Add:
  - Alerts for disk usage (>80%)  

---

### 7. Key Takeaways

- Logs must be:
  - Rotated  
  - Compressed  
  - Cleaned regularly  

- Automation prevents:
  - Disk full issues  
  - System downtime  

---

### 8. Interview-Ready Summary

“To manage large logs without rotation, I would create a cleanup script that compresses logs older than 7 days and deletes logs older than 30 days. I would also log all actions for traceability and schedule the script using cron for automation. In production, I would prefer using logrotate for a more robust and standardized solution.”

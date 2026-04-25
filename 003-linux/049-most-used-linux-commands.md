### Question  
What are 10 Linux commands you use daily? (Excluding basic ones like `ls` and `cd`)

---

### Answer  

---

### 1. `tail -f`

```bash
tail -f /var/log/nginx/error.log
```

- Monitors log files in real time  
- Useful for:
  - Debugging live issues  
  - Tracking errors as they occur  

---

### 2. `grep`

```bash
grep -i "timeout" /var/log/app.log
```

- Searches for patterns in files or output  
- Used to:
  - Filter logs  
  - Find errors quickly  

---

### 3. `systemctl`

```bash
systemctl restart nginx
```

- Manages systemd services  
- Used for:
  - Start / stop / restart services  
  - Check service status  

---

### 4. `journalctl`

```bash
journalctl -u docker.service -f
```

- Views logs for system services  
- Helpful for debugging:
  - Docker  
  - Kubelet  
  - System processes  

---

### 5. `ps aux | grep`

```bash
ps aux | grep nginx
```

- Lists running processes  
- Used to:
  - Find processes  
  - Debug high resource usage  

---

### 6. `df -h` / `du -sh`

```bash
df -h
du -sh *
```

- `df -h` → disk space usage  
- `du -sh` → directory size  

---

### 7. `chmod` / `chown`

```bash
chmod +x deploy.sh
chown ubuntu:ubuntu script.sh
```

- Manage:
  - File permissions  
  - Ownership  

---

### 8. `find`

```bash
find /var/log -name "*.log" -mtime +7
```

- Locate files based on:
  - Name  
  - Time  
  - Type  

- Useful for:
  - Cleanup  
  - Automation  

---

### 9. `curl`

```bash
curl -I http://localhost:8080
```

- Tests APIs and endpoints  
- Used for:
  - Health checks  
  - Debugging services  

---

### 10. `rsync`

```bash
rsync -avz /app/ user@server:/backup/
```

- Efficient file transfer and sync  
- Used for:
  - Backups  
  - Deployments  

---

### 11. Key Takeaways

- These commands help with:
  - Debugging  
  - Monitoring  
  - File management  
  - Networking  
  - Automation  

---

### 12. Interview-Ready Summary

“I regularly use commands like tail and journalctl for log monitoring, grep for searching, systemctl for service management, ps for process inspection, df and du for disk usage, chmod and chown for permissions, find for file discovery, curl for testing endpoints, and rsync for efficient file transfers and backups.”

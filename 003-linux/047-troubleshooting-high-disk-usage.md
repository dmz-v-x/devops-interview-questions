### Question  
Let’s say you get an alert that a filesystem on your production server has high disk usage. How would you debug it?

---

### Answer  

---

### 1. Identify Which Filesystem is Full

```bash
df -h
```

- Shows disk usage by filesystem  
- Identify which mount point (e.g., `/`, `/var`, `/home`) is near 100%  

---

### 2. Check Inode Usage (Important)

```bash
df -i
```

- If inodes are 100%, you cannot create files even if space exists  

---

### 3. Find Large Directories

```bash
du -sh /* 2>/dev/null
```

- Helps identify which top-level directory is consuming space  

---

#### Drill down:

```bash
du -sh /var/* 2>/dev/null
```

---

### 4. Find Large Files

```bash
find / -type f -size +100M -exec ls -lh {} \; 2>/dev/null
```

- Lists files larger than 100MB  

---

### 5. Check Log Files (Very Common Cause)

```bash
du -sh /var/log/*
```

- Logs can grow rapidly (e.g., nginx, syslog, application logs)  

---

#### Clean logs:

```bash
truncate -s 0 /var/log/syslog
```

or

```bash
rm -f /var/log/*.log
```

---

### 6. Check Deleted but Still Open Files

Sometimes files are deleted but still held by a process.

```bash
lsof | grep deleted
```

- These still consume disk space  

---

#### Fix:
- Restart the process holding the file  

---

### 7. Check Temporary Directories

```bash
du -sh /tmp/*
du -sh /var/tmp/*
```

---

#### Clean:

```bash
rm -rf /tmp/*
rm -rf /var/tmp/*
```

---

### 8. Check Docker Usage (if applicable)

```bash
docker system df
```

---

#### Clean:

```bash
docker system prune -af
docker volume prune -f
```

---

### 9. Check Package Cache

```bash
du -sh /var/cache/*
```

---

#### Clean:

```bash
apt clean        # Debian/Ubuntu
yum clean all    # RHEL/CentOS
```

---

### 10. Check for Core Dumps

```bash
find / -name core
```

---

### 11. Check for Backup Files

- Old backups (.tar, .gz, .bak) may consume space  

---

### 12. Verify Mount Issues

- Sometimes disk is mounted incorrectly  

```bash
mount | grep <filesystem>
```

---

### 13. Monitor in Real-Time

```bash
watch df -h
```

---

### 14. Key Debug Flow

1. `df -h` → find full filesystem  
2. `df -i` → check inode usage  
3. `du -sh` → locate large directories  
4. `find` → identify large files  
5. `lsof` → check deleted open files  

---

### 15. Common Root Causes

- Log files growing indefinitely  
- Temporary files accumulation  
- Docker images/containers  
- Backup files  
- Deleted files still in use  
- Too many small files (inode exhaustion)  

---

### 16. Preventive Measures

- Enable log rotation (`logrotate`)  
- Set up monitoring alerts  
- Clean temp files regularly  
- Use separate partitions for logs  
- Use lifecycle policies for backups  

---

### 17. Interview-Ready Summary

“When disk usage is high, I first check df -h to identify the affected filesystem, then df -i to rule out inode issues. Next, I use du to find large directories and files, check logs, temporary files, and Docker usage. I also verify if any deleted files are still open using lsof. Once identified, I clean up safely and implement preventive measures like log rotation and monitoring.”

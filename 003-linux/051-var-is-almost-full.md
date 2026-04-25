### Question  
`/var` is almost 90% full. What will be your next steps?

---

### Answer  

---

### 1. High-Level Approach

- Identify what is consuming space  
- Clean unnecessary files  
- Prevent recurrence  

---

### 2. Step 1: Analyze Disk Usage

```bash
sudo du -sh /var/* | sort -hr | head -10
```

---

#### Goal:

- Find largest directories:
  - `/var/log`  
  - `/var/cache`  
  - `/var/lib/docker`  

---

### 3. Step 2: Clean Log Files

---

#### If `/var/log` is large:

```bash
sudo journalctl --vacuum-size=200M
```

---

#### Remove old rotated logs:

```bash
sudo rm -rf /var/log/*.gz /var/log/*.[0-9]
```

---

#### Truncate large logs:

```bash
sudo truncate -s 0 /var/log/syslog
```

---

### 4. Step 3: Clear Package Cache

---

#### Debian/Ubuntu:

```bash
sudo apt clean
```

---

#### RHEL/CentOS:

```bash
sudo yum clean all
```

---

### 5. Step 4: Check Docker Usage

```bash
docker system df
```

---

#### Cleanup:

```bash
docker system prune -a
```

---

#### Warning:

- Removes unused images/containers/volumes  
- Be cautious in production  

---

### 6. Step 5: Archive or Move Data

- Move old logs to:
  - `/home`  
  - S3 / external storage  

---

#### Configure log rotation:

```bash
sudo nano /etc/logrotate.conf
```

---

### 7. Step 6: Set Up Monitoring & Alerts

- Tools:
  - `ncdu`  
  - `duf`  
  - Prometheus + Grafana  

---

- Set alerts for:
  - Disk usage thresholds  

---

### 8. Common Causes of `/var` Filling Up

- Excessive logging  
- Docker images and containers  
- Package cache buildup  
- Crash dumps or mail spools  

---

### 9. Key Takeaways

- Always:
  - Identify → Clean → Prevent  
- Logs and Docker are common culprits  
- Monitoring avoids future incidents  

---

### 10. Interview-Ready Summary

“If /var is 90% full, I first identify large directories using du. Then I clean logs, clear package caches, and check Docker usage if applicable. I may archive old data and configure log rotation. Finally, I set up monitoring and alerts to prevent recurrence.”

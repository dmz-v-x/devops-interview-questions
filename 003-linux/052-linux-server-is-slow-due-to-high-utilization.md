### Question  
Linux Server is slow due to high CPU utilization. How will you fix it?

---

### Answer  

---

### 1. Initial Understanding

- High CPU usage leads to:
  - Slow response times  
  - System lag  
  - Delayed processing  

- Objective:
  - Identify **which process is consuming CPU**
  - Fix the **root cause**, not just symptoms  

---

### 2. Check Load Average

```bash
uptime
```

**Example Output:**
    14:02:03 up 3 days, 4:55, 2 users, load average: 6.02, 4.33, 2.89

- Load average represents system load over:
  - 1 min  
  - 5 min  
  - 15 min  

- If load average > number of CPU cores → **CPU is overloaded**

---

### 3. Identify CPU-Heavy Processes

```bash
top -o %CPU
```

OR:

```bash
htop
```

- Shows:
  - Real-time CPU usage  
  - Top CPU-consuming processes  

- Helps identify:
  - Runaway processes  
  - Misbehaving applications  

---

### 4. Drill Down with Detailed Tools

```bash
ps -eo pid,ppid,cmd,%cpu,%mem --sort=-%cpu | head
```

OR:

```bash
pidstat -u 1 5
```

- `ps` → Snapshot of top CPU consumers  
- `pidstat` → CPU usage over time  

---

### 5. Investigate the Cause

- Analyze based on findings:

  - Is it a specific application? (Java, Python, Node.js)  
  - Is a cron job or batch process running?  
  - Is a service stuck in a loop?  
  - Is it a bug (e.g., zombie processes)?  

---

### 6. Take Corrective Action

- Kill runaway process:

```bash
kill -9 <pid>
```

- Restart service:

```bash
systemctl restart <service>
```

- Additional actions:

  - Scale application / distribute workload  
  - Optimize queries or code  
  - Fix memory leaks  
  - Apply patches for known bugs  

- Limit CPU usage:

```bash
nice -n 10 <command>
cpulimit -p <pid> -l 50
```

---

### 7. Check Logs

```bash
journalctl -xe
```

```bash
tail -f /var/log/syslog
```

- Look for:
  - Application crashes  
  - Infinite loops / retries  
  - Misconfigurations  

---

### 8. Implement Preventive Measures

- Set resource limits:
  - cgroups / container limits  

- Monitoring:
  - Prometheus + Grafana  

- Alerts:
  - CPU usage > 80% for sustained time  

- Optimization:
  - Refactor heavy tasks  
  - Schedule jobs during off-peak hours  

---

### 9. Key Takeaways

- Follow approach:
  - Identify → Analyze → Fix → Prevent  

- Common causes:
  - Poorly optimized code  
  - Misconfiguration  
  - Unexpected workload  

---

### 10. Interview-Ready Summary

“I would first check system load using uptime, then identify CPU-intensive processes using top or htop. Next, I’d analyze them using ps or pidstat to find the root cause, whether it’s a misbehaving application, cron job, or bug. Based on that, I’d take corrective actions like killing processes, restarting services, or optimizing workloads. Finally, I’d check logs and implement monitoring and alerts to prevent recurrence.”

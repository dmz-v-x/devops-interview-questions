### Question  
User reports slowness in the application. How would you approach this?

---

### Answer  

I follow a **layered debugging approach** starting from system-level checks to application-level investigation.

---

### 1. Check Server Resource Utilization

If the application is running on a VM:

```bash
top
htop
```

- Check:
  - CPU utilization  
  - Memory usage  
  - Disk usage  

---

#### Additional tools:

```bash
vmstat
iostat
```

- Helps identify:
  - CPU bottlenecks  
  - Memory pressure  
  - Disk I/O issues  

---

#### If high usage is found:

- Identify heavy processes  
- Kill or deprioritize non-critical processes  

---

### Kubernetes Scenario

- Kubernetes runs on VMs → same checks apply  

Additionally:

- Use observability tools:
  - Prometheus  
  - Grafana  

- Check:
  - Pod resource usage  
  - Node pressure  

---

#### Fix:

- Scale:
  - Horizontal Pod Autoscaler (HPA)  
  - Increase resources  

---

### 2. Check Network Latency

```bash
ping <host>
traceroute <host>
```

- Helps identify:
  - Delays in response  
  - Network hops  

---

#### Fix:

- Use CDN  
- Deploy app closer to users (region optimization)  

---

### 3. Check Bandwidth Issues

```bash
iftop
nload
```

- Identify:
  - Network saturation  
  - High traffic  

---

### 4. Check Application Logs

- Look at:
  - Error logs  
  - System logs  

```bash
tail -f /var/log/app.log
```

- Identify:
  - Slow functions  
  - Exceptions  
  - Thread issues  

---

### 5. Check Open Connections

```bash
netstat -tulnp
```

- Look for:
  - Too many connections  
  - Stuck sockets  

---

#### Fix:

- Close unnecessary connections  
- Tune connection limits  

---

### 6. Check Container / Pod Limits

- Ensure:
  - CPU/memory limits are not throttling pods  

---

### 7. Rollbacks or Restarts

If issue started after deployment:

- Rollback release  
- Restart pods/services  

---

### 8. Key Debug Flow

1. Check CPU, memory, disk  
2. Check Kubernetes resources (if applicable)  
3. Check network latency  
4. Check bandwidth  
5. Check logs  
6. Check connections  

---

### 9. Common Causes

- High CPU or memory usage  
- Disk I/O bottlenecks  
- Network latency  
- Bandwidth saturation  
- Application bugs  
- Too many connections  
- Resource limits  

---

### 10. Interview-Ready Summary

“When a user reports slowness, I start by checking system resources like CPU, memory, and disk using top and iostat. If it's Kubernetes, I also check pod metrics using tools like Prometheus. Then I check network latency using ping and traceroute, followed by bandwidth usage. If infrastructure looks fine, I analyze application logs and check for excessive connections. If the issue started after a deployment, I consider rollback or restart. This layered approach helps quickly isolate the root cause.”

### Question  
How do you check Docker container resource utilization?

---

### Answer  

### 1. Using `docker stats` (Most Common Method)  

The `docker stats` command shows **real-time resource usage** of running containers.

---

#### Basic Command  

    docker stats

---

#### Example Output  

    CONTAINER ID   NAME       CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O
    a1b2c3d4       my-nginx   0.25%     15MiB / 512MiB        2.9%      1kB / 2kB     0B / 0B

---

### 2. Metrics Explained  

---

| Metric | Description |
|---|---|
| CPU % | CPU usage of container |
| MEM USAGE | Memory used / total available |
| MEM % | Memory usage percentage |
| NET I/O | Network data sent/received |
| BLOCK I/O | Disk read/write |
| PIDS | Number of processes |

---

### 3. Monitor Specific Container  

    docker stats <container-name>

---

#### Example  

    docker stats my-nginx

---

### 4. Run Once (Non-Streaming Mode)  

By default, `docker stats` runs continuously.

To get a one-time snapshot:

    docker stats --no-stream

---

### 5. Format Output (Optional)  

    docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"

---

### 6. Key Concept  

- Shows **live performance metrics**  
- Useful for:
  - Debugging  
  - Performance tuning  
  - Monitoring  

---

### 7. Real-World Use Cases  

---

Check high CPU usage container  

---

Detect memory leaks  

---

Monitor production workloads  

---

---

### 8. Tricky Interview Questions  

---

Does `docker stats` show stopped containers?  

- ❌ No (only running containers)  

---

Is this real-time monitoring?  

- ✅ Yes  

---

What if no containers are running?  

- No output shown  

---

How to limit container resources?  

    docker run -m 512m --cpus="1.0" myapp

---

### Interview Summary  

The `docker stats` command provides real-time insights into container resource usage such as CPU, memory, network, and disk I/O. It is an essential tool for monitoring container performance and diagnosing resource-related issues.

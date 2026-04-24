### Question  
EC2 High CPU Utilization — How would you troubleshoot and resolve it?

---

### 1. Overview

High CPU utilization on an EC2 instance can lead to:
- Slow application performance  
- Timeouts or failures  
- Resource exhaustion  

The goal is to **identify the cause and apply scaling or optimization**.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check CloudWatch Metrics

- Go to:
  - EC2 → Monitoring (CloudWatch)  

#### Analyze:
- CPU utilization trends  
- Sudden spikes or sustained high usage  

---

### 2.2 Identify High CPU Processes

```bash
top
```

or

```bash
htop
```

#### Purpose:
- Find processes consuming excessive CPU  

---

### 2.3 Analyze Root Cause

- Application issues:
  - Infinite loops  
  - Inefficient queries  
- Background jobs or cron tasks  
- Traffic spikes  

---

### 2.4 Take Immediate Action

- Restart problematic processes  
- Kill runaway processes if necessary  

---

### 2.5 Optimize Application

- Improve code efficiency  
- Optimize database queries  
- Add caching mechanisms  

---

### 3. Scaling Solutions

---

### 3.1 Vertical Scaling

- Upgrade instance type:
  - More CPU/RAM  

---

### 3.2 Horizontal Scaling

- Use Auto Scaling Group  
- Add more instances based on CPU thresholds  

---

### 4. Additional Checks

- Check load balancer distribution  
- Ensure no DDoS or abnormal traffic  
- Monitor background services  
- Review logs for anomalies  

---

### 5. Key Takeaways

- Always identify root cause before scaling  
- Use monitoring tools like CloudWatch  
- Combine optimization with scaling  
- Automate scaling for production systems  

---

### 6. Interview-Ready Summary

“If an EC2 instance has high CPU utilization, I first check CloudWatch metrics to identify patterns or spikes. Then I use tools like top or htop to find which processes are consuming CPU. Based on the root cause, I either restart or optimize the application. If the workload is legitimate, I scale vertically by upgrading the instance or horizontally using Auto Scaling to handle increased demand efficiently.”

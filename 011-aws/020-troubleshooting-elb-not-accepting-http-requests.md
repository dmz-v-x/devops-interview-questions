### Question  
ELB not accepting HTTPS requests — How would you troubleshoot?

---

### 1. Overview

If an Elastic Load Balancer (ELB) is not accepting HTTPS (port 443) requests, the issue is usually related to:
- SSL/TLS configuration  
- Listener setup  
- Security rules  
- Backend configuration  

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Verify SSL Certificate (ACM)

- Go to:
  - AWS Certificate Manager (ACM)  

#### Check:
- Certificate is:
  - Issued (not pending)  
  - Valid  
- Attached to ELB  

---

### 2.2 Check Security Group Rules

#### ELB Security Group:
- Allow inbound:
```bash
Port: 443 (HTTPS)
Source: 0.0.0.0/0 (or restricted range)
```

#### Instance Security Group:
- Allow traffic from ELB  

---

### 2.3 Verify Listener Configuration

- Go to:
  - Load Balancer → Listeners  

#### Ensure:
- Listener exists:
```bash
Protocol: HTTPS
Port: 443
```

- SSL certificate is selected  
- Correct target group is configured  

---

### 2.4 Check Backend Instance Configuration

- Ensure instances:
  - Are running  
  - Accept traffic on expected port  

#### Note:
- If using HTTPS backend:
  - Instances must support SSL  

---

### 2.5 Check Health Checks

- Target group health check must pass  

#### Verify:
- Correct path  
- Correct port  

---

### 2.6 Check Logs and Metrics

- CloudWatch:
  - Error rates  
  - Request count  

- CloudTrail:
  - SSL-related configuration changes  

---

### 3. Additional Checks

- Certificate domain matches request hostname  
- SSL policy compatibility (TLS versions)  
- DNS pointing correctly to ELB  
- Browser/client SSL errors  

---

### 4. Key Takeaways

- HTTPS requires valid SSL certificate  
- Listener must be correctly configured  
- Security groups must allow port 443  
- Backend must be reachable and healthy  

---

### 5. Interview-Ready Summary

“If ELB is not accepting HTTPS requests, I first verify that a valid SSL certificate from ACM is attached to the load balancer. Then I check that port 443 is allowed in the security group and that the HTTPS listener is correctly configured. I also ensure backend instances are healthy and accepting traffic. Finally, I review CloudWatch and CloudTrail logs to identify any SSL-related errors.”

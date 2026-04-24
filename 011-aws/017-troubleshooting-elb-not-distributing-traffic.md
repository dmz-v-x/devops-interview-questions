### Question  
Elastic Load Balancer (ELB) is not distributing traffic — How would you troubleshoot?

---

### 1. Overview

If an ELB is not distributing traffic properly, the issue is usually related to:
- Target health  
- Networking configuration  
- Listener setup  
- Target registration  

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Target Health

- Navigate:
  - EC2 → Load Balancers → Target Groups → Health Status  

#### Verify:
- Targets are **healthy**  

#### If unhealthy:
- Check:
  - Health check path  
  - Application status  
  - Port configuration  

---

### 2.2 Verify Security Groups and NACLs

#### ELB Security Group:
- Allow inbound traffic:
  - HTTP (80) / HTTPS (443) from internet  

#### Instance Security Group:
- Allow inbound traffic from:
  - ELB security group  

#### NACLs:
- Ensure inbound/outbound traffic is allowed  

---

### 2.3 Check Listener Configuration

- Navigate:
  - Load Balancer → Listeners  

#### Verify:
- Correct protocol (HTTP/HTTPS)  
- Correct port (80/443)  
- Forwarding rules mapped to correct target group  

---

### 2.4 Verify Target Registration

- Ensure instances are:
  - Registered in target group  
  - In correct availability zones  

---

### 2.5 Check CloudWatch Metrics

- Monitor:
  - RequestCount  
  - HealthyHostCount  
  - UnHealthyHostCount  
  - Latency  

#### Purpose:
- Identify traffic patterns and anomalies  

---

### 3. Additional Checks

- Application is running on correct port  
- Health check endpoint is accessible  
- Instances are not overloaded  
- Cross-zone load balancing enabled (if required)  

---

### 4. Key Takeaways

- Healthy targets are essential  
- Security groups must allow traffic flow  
- Listeners must be configured correctly  
- Monitoring helps identify issues quickly  

---

### 5. Interview-Ready Summary

“If ELB is not distributing traffic, I first check the health status of target instances to ensure they are healthy. Then I verify security groups and NACLs to ensure proper traffic flow between the load balancer and instances. I check listener configuration to confirm correct ports and forwarding rules. I also ensure instances are properly registered in the target group and monitor CloudWatch metrics to analyze traffic behavior. This helps identify and resolve the issue efficiently.”

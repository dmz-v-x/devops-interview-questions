### Question  
Why might an Auto Scaling Group (ASG) not launch EC2 instances, and how would you troubleshoot it?

---

### Answer  

---

### 1. Overview

- ASG depends on:
  - Launch Template / Configuration  
  - Networking  
  - IAM permissions  
  - Capacity & scaling policies  

- If any of these fail → **instances won’t launch**  

---

### 2. Common Reasons

---

#### 1. Launch Template / AMI Issues

- Invalid or deleted AMI  
- Unsupported instance type in AZ  
- Misconfigured launch template  

---

#### 2. Networking Issues

- No subnets configured  
- Subnet has no available IPs  
- Incorrect route tables  
- Security groups blocking traffic  

---

#### 3. IAM Role Issues

- Missing instance profile  
- Insufficient permissions  
- Cannot access required services (SSM, EFS, etc.)  

---

#### 4. Capacity & Limits

- EC2 quota exceeded  
- Instance type unavailable in AZ  
- Spot capacity unavailable  

---

#### 5. Scaling Configuration

- Desired capacity = 0  
- Scaling policies reducing capacity  
- Scheduled scaling actions  

---

#### 6. Bootstrapping / Health Check Failures

- User data script fails  
- App not starting  
- ELB/EC2 health checks failing  

- Result:
  - Instances launch → fail → terminated repeatedly  

---

### 3. Step-by-Step Troubleshooting

---

#### Step 1: Check Desired Capacity

```text
EC2 → Auto Scaling Groups → Desired Capacity
```

- If `0`:
  - ASG is working as expected  

---

#### Step 2: Check ASG Activity History

- Look for errors like:
  - "AMI not found"  
  - "Capacity error"  
  - "Not authorized"  

---

#### Step 3: Validate Launch Template

- Verify:
  - AMI exists  
  - Instance type supported  
  - Correct configuration  

- Test:
  - Switch to On-Demand if using Spot  

---

#### Step 4: Check Networking

- Ensure:
  - Subnets are configured  
  - Subnets have free IPs  

- Verify routes:
  - Public → IGW  
  - Private → NAT (if needed)  

---

#### Step 5: Verify IAM Role

- Check:
  - Instance profile attached  

- Ensure:
  - Required permissions exist  

---

#### Step 6: Debug EC2 Instances

- Check:
  - System logs  

```text
EC2 → Instance → Actions → Get System Log
```

- Review:
  - User Data script  
  - Application startup  

---

#### Step 7: Check Service Limits

- Go to:
  - AWS Service Quotas  

- Verify:
  - vCPU limits  
  - Instance limits  

---

### 4. Example Failure Scenarios

- Invalid AMI:
  - Fix → Update launch template  

- No capacity:
  - Fix → Change AZ or instance type  

- Subnet full:
  - Fix → Use different subnet  

- IAM issue:
  - Fix → Attach proper role  

- Health check failure:
  - Fix → Debug app + increase grace period  

---

### 5. Key Takeaways

- Most common reasons:
  - Misconfiguration  
  - Capacity issues  
  - Health check failures  

- Always start with:
  - **ASG Activity History**  

---

### 6. Interview-Ready Summary

“If an ASG is not launching instances, I start by checking the desired capacity and ASG activity history to identify errors. Then I verify the launch template, ensuring the AMI and instance type are valid. Next, I check networking, IAM roles, and service quotas. If instances are launching but failing, I inspect system logs and user data scripts for errors. This systematic approach helps quickly identify and resolve the issue.”

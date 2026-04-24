### Question  
EC2 Instance is Not Starting — How would you troubleshoot?

---

### 1. Overview

If an EC2 instance is not starting, the issue can be related to:
- Permissions  
- Resource limits  
- Instance configuration  
- OS/boot-level failures  

A systematic troubleshooting approach helps identify the root cause quickly.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Instance Status in AWS Console

- Go to:
  - EC2 → Instances  
- Verify:
  - Instance state (pending, stopped, running)  
  - Status checks (2/2 checks passed)

---

### 2.2 Check Permissions (IAM)

- Ensure you have required permissions:
  - `ec2:StartInstances`  
- Verify IAM role or user policy  

---

### 2.3 Verify Instance Limits and Type

- Check if:
  - Instance type is supported in the region  
  - Account limits (vCPU limits) are not exceeded  

---

### 2.4 Check System Logs

- Navigate:
  - EC2 → Actions → Monitor and Troubleshoot → Get System Log  

- Look for:
  - Kernel errors  
  - Boot failures  
  - Disk/mount issues  

---

### 2.5 Check Status Checks

- **System Status Check** → AWS infrastructure issue  
- **Instance Status Check** → OS-level issue  

---

### 2.6 Troubleshoot Boot Volume (Advanced)

If boot corruption is suspected:

#### Steps:
1. Stop the instance  
2. Detach root volume  
3. Attach volume to another working instance  
4. Inspect logs:

```bash
/var/log/messages
/var/log/syslog
```

5. Fix issues and reattach  

---

### 3. Additional Checks

- Security group / network misconfiguration  
- Incorrect AMI or launch configuration  
- Corrupted file system  
- User data script failures  

---

### 4. Key Takeaways

- Always start with AWS console checks  
- Use system logs for deeper debugging  
- Verify permissions and limits  
- Use volume recovery for OS-level issues  

---

### 5. Interview-Ready Summary

“If an EC2 instance is not starting, I first check its status and health checks in the AWS console. Then I verify IAM permissions and ensure instance limits are not exceeded. I review system logs to identify boot or kernel issues. If I suspect a corrupted root volume, I detach it, attach it to another instance, inspect logs, fix the issue, and reattach it. This step-by-step approach helps isolate whether the issue is infrastructure, configuration, or OS-related.”

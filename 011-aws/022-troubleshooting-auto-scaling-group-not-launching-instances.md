### Question  
Auto Scaling Group (ASG) not launching instances — How would you troubleshoot?

---

### 1. Overview

If an Auto Scaling Group is not launching instances, the issue is usually related to:
- Launch configuration/template issues  
- Capacity or quota limits  
- Network/subnet problems  
- Scaling policy misconfiguration  

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Launch Template / Launch Configuration

- Verify:
  - AMI ID is correct and exists  
  - Instance type is valid  
  - Key pair and security groups are correctly defined  

#### Common Issues:
- Invalid AMI  
- Missing permissions  

---

### 2.2 Verify Instance Limits (Quotas)

- Check AWS limits:
  - vCPU limits  
  - Instance type availability  

#### Action:
- Request limit increase if exceeded  

---

### 2.3 Validate AMI Accessibility

- Ensure:
  - AMI is not deleted  
  - AMI is shared (if cross-account)  

---

### 2.4 Check Subnet and IP Availability

- Ensure:
  - Subnets have available IP addresses  
  - Subnets are correctly associated with ASG  

#### Common Issue:
- Subnet exhausted → no instance launch  

---

### 2.5 Review Scaling Policies & CloudWatch Alarms

- Check:
  - Scaling policies are triggered correctly  
  - CloudWatch alarms are firing  

#### Verify:
- Metrics thresholds  
- Alarm state  

---

### 3. Additional Checks

- IAM role attached to ASG has required permissions  
- Capacity constraints in Availability Zones  
- Spot instance limitations (if used)  
- Check activity history:
  - EC2 → Auto Scaling Groups → Activity  

---

### 4. Key Takeaways

- Launch template errors are most common  
- Subnet IP exhaustion is often overlooked  
- CloudWatch alarms must trigger scaling  
- Always check ASG activity logs  

---

### 5. Interview-Ready Summary

“If an Auto Scaling Group is not launching instances, I first check the launch template or configuration for errors such as invalid AMI or incorrect instance type. Then I verify AWS limits and ensure the AMI is accessible. I also check whether the subnets have available IP addresses and are correctly configured. Finally, I review scaling policies and CloudWatch alarms to ensure scaling conditions are being triggered. Checking the ASG activity history helps identify the exact failure reason.”

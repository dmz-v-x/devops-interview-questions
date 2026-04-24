### Question  
EC2 Instance Terminated Unexpectedly — How would you troubleshoot and recover?

---

### 1. Overview

Unexpected EC2 termination can occur due to:
- Manual actions  
- Auto Scaling policies  
- Spot interruptions  
- Billing or limit issues  

The goal is to **identify the cause and recover quickly**.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check CloudTrail Logs

- Go to:
  - AWS CloudTrail → Event History  

#### Look for:
- `TerminateInstances` event  
- Who/what triggered the termination  

---

### 2.2 Verify Auto Scaling Configuration

- Check if instance is part of:
  - Auto Scaling Group (ASG)  

#### Possible reasons:
- Health check failure  
- Scaling policy triggered  

---

### 2.3 Check Spot Instance / Pricing

- If using Spot Instances:
  - Instance may be terminated due to price changes  

#### Check:
- Spot interruption notices  

---

### 2.4 Check Billing / Limits

- Verify:
  - AWS account billing status  
  - Instance quota limits  

---

### 2.5 Review Termination Protection

- Check if:
  - Termination protection was enabled  

#### If disabled:
- Instance can be terminated accidentally  

---

### 3. Recovery Steps

---

### 3.1 Restore from AMI

- Launch new instance from:
  - Existing AMI  

---

### 3.2 Restore from Snapshot

- Create volume from snapshot  
- Attach to new instance  

---

### 3.3 Recreate Environment

- Use:
  - Infrastructure as Code (Terraform/CloudFormation)  
- Helps quick recovery  

---

### 4. Prevention Best Practices

- Enable termination protection  
- Use Auto Scaling with proper health checks  
- Take regular snapshots/AMIs  
- Monitor with CloudWatch and alerts  
- Avoid using Spot instances for critical workloads  

---

### 5. Key Takeaways

- Use CloudTrail to find root cause  
- Check ASG and Spot settings  
- Always have backup (AMI/snapshots)  
- Automate recovery where possible  

---

### 6. Interview-Ready Summary

“If an EC2 instance is terminated unexpectedly, I first check CloudTrail logs to identify who or what triggered the termination. Then I verify if the instance was part of an Auto Scaling group or a Spot instance, as these can automatically terminate instances. I also check billing and termination protection settings. For recovery, I launch a new instance from an AMI or snapshot. To prevent this in the future, I enable termination protection, use proper monitoring, and maintain regular backups.”

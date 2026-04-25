### Question  
An EC2 instance terminated unexpectedly. How would you handle it?

---

### Answer  

---

### 1. Immediate Action (Stabilize & Assess Impact)

- Confirm termination:
  - EC2 Console  
  - CloudTrail logs  

- Identify:
  - Was it intentional or unexpected?  

- Check:
  - Impact on application/services  

- Communicate:
  - Notify stakeholders if production is affected  

---

### 2. Troubleshooting (Find Root Cause)

---

#### Check Logs & Events

- CloudTrail:
  - Who/what triggered termination  

- EC2 State Transition Reason:
  - Example:
    - User initiated  
    - Instance retired  
    - Spot interruption  

---

#### Common Causes

- Human error:
  - Manual termination  

- Automation:
  - Auto Scaling / ECS / CloudFormation  

- Spot Instance:
  - Reclaimed by AWS  

- AWS Maintenance:
  - Hardware failure / retirement  

- Misconfiguration:
  - Lifecycle policies  

- System failure:
  - Rare cases (kernel/disk issues)  

---

### 3. Recovery (Restore Service)

- If using Auto Scaling:
  - Verify new instance launched  
  - Check launch template/config  

---

- If standalone instance:

```text
- Relaunch from AMI
- Restore from EBS snapshot
- Attach old EBS volume (if retained)
```

---

- If Spot instance:
  - Switch to:
    - On-Demand  
    - Spot with better strategy  

---

- If using IaC:
  - Redeploy using:
    - Terraform  
    - CloudFormation  

---

### 4. Prevention (Avoid Future Issues)

---

#### Access Control

- Enforce:
  - IAM least privilege  

---

#### Enable Protection

```text
DisableApiTermination = true
```

---

#### Auto Scaling Best Practices

- Proper health checks  
- Correct launch templates  
- Multi-AZ deployment  

---

#### Spot Best Practices

- Use:
  - Capacity-optimized strategy  
  - On-Demand fallback  

---

#### Monitoring & Alerts

- CloudWatch alarms  
- SNS / Slack alerts  

---

#### Backup Strategy

- Regular:
  - AMIs  
  - EBS snapshots  

---

#### Governance

- AWS Config rules  
- Guardrails for critical resources  

---

### 5. Key Takeaways

- Always:
  - Identify root cause first  
  - Recover quickly using automation  

- Prevent using:
  - IAM  
  - Monitoring  
  - Auto Scaling  
  - Backups  

---

### 6. Interview-Ready Summary

“If an EC2 instance terminates unexpectedly, I first check CloudTrail and the EC2 state transition reason to identify the cause—whether it’s user action, Auto Scaling, Spot interruption, or AWS maintenance. Then I restore the service using Auto Scaling or by relaunching from AMIs or snapshots. To prevent recurrence, I enforce IAM least privilege, enable termination protection, configure Auto Scaling properly, and set up monitoring and alerts. I also ensure backups and Infrastructure as Code are in place for quick recovery.”

### Question  
SSH to an instance stopped working. How will you troubleshoot the issue?

---

### Answer  

---

### 1. Understand the Error Message

- Run from local machine:

```bash
ssh -i my-key.pem ec2-user@<instance-public-ip>
```

- Common errors:

  - `Permission denied (publickey)` → Key or username issue  
  - `Connection refused` → SSH service not running  
  - `Operation timed out` → Network/firewall issue  

- The error message gives the **initial debugging direction**  

---

### 2. Verify Instance Status & Reachability

```bash
aws ec2 describe-instance-status --instance-id <id>
```

```bash
ping <public-ip>
```

- Check:
  - Instance is **running**  
  - Status checks passed (2/2)  

- If unreachable:
  - Investigate:
    - VPC configuration  
    - Subnet  
    - Route tables  

---

### 3. Verify Public IP / Elastic IP

- Ensure instance has:
  - Public IP OR  
  - Elastic IP  

- Important:
  - Public IP changes after stop/start  
  - Elastic IP remains constant  

---

### 4. Check Security Group Rules

- Ensure inbound rule:

    Type: SSH  
    Port: 22  
    Source: Your IP (e.g., x.x.x.x/32)

- If using bastion host:
  - Verify its connectivity as well  

---

### 5. Check Network ACLs & Routing

- Ensure:
  - NACL allows inbound/outbound traffic  
  - Subnet has route to Internet Gateway  

- Misconfigured NACL can silently block traffic  

---

### 6. Validate PEM File & Username

- Check permissions:

```bash
chmod 400 my-key.pem
```

- Ensure correct username:

  - Amazon Linux → `ec2-user`  
  - Ubuntu → `ubuntu`  
  - CentOS → `centos`  

- Also verify:
  - Correct PEM file is being used  
  - Correct IP address is used  

---

### 7. Check SSH Service on Instance

(If access via SSM or console is available)

```bash
sudo systemctl status ssh
```

- If not running:

```bash
sudo systemctl restart ssh
```

- If SSH service is down → connection will be refused  

---

### 8. Check Firewall Inside Instance

```bash
sudo ufw status
```

- Ensure port 22 is allowed  

- Also check:

```bash
sudo iptables -L
```

---

### 9. Additional Debugging

- Check system resources:

```bash
df -h
```

```bash
top
```

- Issues like:
  - Full disk  
  - High CPU/memory  

- Can prevent SSH access  

- Check logs:

```bash
sudo journalctl -u ssh
```

---

### 10. Recovery Options

- Use:
  - EC2 Instance Connect  
  - SSM Session Manager  

- If no access:
  - Detach root volume  
  - Attach to another instance  
  - Fix `authorized_keys`  

---

### 11. Key Takeaways

- Debug flow:
  - Error → Network → Access → Service → System  

- Most common causes:
  - Wrong key or permissions  
  - Security group misconfiguration  
  - SSH service down  
  - IP address change  

---

### 12. Interview-Ready Summary

“I would start by checking the SSH error message to identify whether it’s a key, network, or service issue. Then I’d verify the instance is running and reachable, ensure the correct public IP is used, and check that port 22 is open in the security group and not blocked by NACLs. Next, I’d validate the PEM file permissions and username. If needed, I’d check whether the SSH service is running and inspect firewall rules. If access is still not possible, I’d use SSM or a volume rescue method to restore access.”

### Question  
Unable to SSH into EC2 Instance — How would you troubleshoot?

---

### 1. Overview

SSH access issues to an EC2 instance are usually caused by:
- Network misconfiguration  
- Incorrect security rules  
- Key or authentication issues  
- OS-level problems  

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Security Group Rules

- Ensure inbound rule allows SSH:

```bash
Port: 22
Source: Your IP (x.x.x.x/32) or trusted range
```

#### Purpose:
- Without this, SSH connection will be blocked  

---

### 2.2 Verify Public IP / Elastic IP

- Check if instance has:
  - Public IP OR  
  - Elastic IP  

#### Note:
- Required for internet-based SSH access  

---

### 2.3 Check Key Pair

- Ensure:
  - Correct key pair is used  
  - `.pem` file matches instance key  

#### Correct command:
```bash
ssh -i key.pem ec2-user@<public-ip>
```

---

### 2.4 Check Network Configuration

- Ensure:
  - Internet Gateway attached to VPC  
  - Route table includes:
  
```bash
0.0.0.0/0 → Internet Gateway
```

---

### 2.5 Use EC2 Serial Console (Advanced Debugging)

- Access instance via:
  - EC2 → Connect → Serial Console  

#### Useful for:
- Fixing SSH config  
- Checking system-level issues  

---

### 2.6 Restart the Instance

- Reboot instance:

```bash
Reboot Instance
```

#### Purpose:
- Resolve temporary issues  

---

### 3. Additional Checks

- File permissions:
```bash
chmod 400 key.pem
```

- Username correctness:
  - Amazon Linux → ec2-user  
  - Ubuntu → ubuntu  

- SSH service running:
```bash
sudo systemctl status sshd
```

- Disk full or OS crash  

---

### 4. Key Takeaways

- Security groups and keys are most common causes  
- Network configuration must allow access  
- Serial console helps in deep debugging  
- Restart can fix transient issues  

---

### 5. Interview-Ready Summary

“If I’m unable to SSH into an EC2 instance, I first check the security group to ensure port 22 is open to my IP. Then I verify that the instance has a public or elastic IP and that I’m using the correct key pair. I also check route tables and internet gateway configuration. If SSH still fails, I use the EC2 serial console to debug OS-level issues. Finally, I restart the instance to rule out temporary problems.”

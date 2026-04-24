### Question  
You have a private subnet in your VPC that contains instances without direct internet access. You still need secure administrative access. How would you set up a bastion host?

---

### 1. Overview

A **Bastion Host (Jump Host)** is a secure entry point that allows administrators to access instances in a private subnet without exposing them to the internet.

---

### 2. Architecture Design

- Public Subnet:
  - Bastion Host (EC2 with public IP)

- Private Subnet:
  - Application/DB instances (no public IP)

- Access Flow:
  - Admin → Bastion Host → Private Instances

---

### 3. Step-by-Step Setup

---

### 3.1 Launch Bastion Host in Public Subnet

- Create an EC2 instance in **public subnet**  
- Assign:
  - Public IP or Elastic IP  

---

### 3.2 Configure Bastion Host Security Group

Allow inbound access only from trusted sources:

#### Example:
- Allow SSH (22) from:
  - Your IP address (e.g., `x.x.x.x/32`)  

#### Outbound:
- Allow traffic to private subnet  

---

### 3.3 Configure Private Instance Security Group

Allow access **only from bastion host**:

#### Example:
- Allow SSH (22) from:
  - Bastion Host Security Group  

---

### 3.4 Access Workflow

#### Step 1: Connect to Bastion Host
```bash
ssh -i key.pem ec2-user@<bastion-public-ip>
```

#### Step 2: Connect to Private Instance
```bash
ssh -i key.pem ec2-user@<private-ip>
```

---

### 4. Optional Enhancements

---

### 4.1 Use SSH Agent Forwarding

```bash
ssh -A ec2-user@<bastion-ip>
```

- Avoid copying private keys to bastion  

---

### 4.2 Use ProxyJump (Simplified Access)

```bash
ssh -i key.pem -J ec2-user@<bastion-ip> ec2-user@<private-ip>
```

---

### 4.3 Logging and Monitoring

- Enable:
  - CloudWatch Logs  
  - VPC Flow Logs  

---

### 4.4 Alternative (Modern Approach)

- Use **AWS Systems Manager Session Manager**
  - No bastion required  
  - No SSH exposure  
  - Fully managed and secure  

---

### 5. Security Best Practices

- Restrict SSH access to specific IPs  
- Use key-based authentication (no passwords)  
- Rotate keys regularly  
- Disable root login  
- Monitor access logs  

---

### 6. Key Takeaways

- Bastion host acts as a secure gateway  
- Only public-facing instance  
- Private instances remain isolated  
- Security groups enforce controlled access  

---

### 7. Interview-Ready Summary

“To securely access instances in a private subnet, I would set up a bastion host in a public subnet with a public IP. I would restrict access to the bastion host using security groups to allow SSH only from trusted IPs. Then, I would configure private instances to allow SSH only from the bastion host’s security group. Administrators would first connect to the bastion host and then access private instances using their private IPs. For enhanced security, I can also use AWS Systems Manager Session Manager as a modern alternative to avoid exposing SSH altogether.”

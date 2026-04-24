### Question  
You have a VPC with a public subnet and a private subnet. Instances in the private subnet need to access the internet for software updates. How would you allow internet access for instances in the private subnet?

---

### 1. Overview

Instances in a **private subnet** do not have direct internet access.  
To enable **outbound internet access (without exposing them publicly)**, we use:

- NAT Gateway (recommended)  
- NAT Instance (older approach)  

---

### 2. Solution Design

---

### 2.1 Use NAT Gateway (Recommended)

#### Step 1: Create NAT Gateway
- Place NAT Gateway in **public subnet**  
- Attach an **Elastic IP**  

---

### 2.2 Configure Public Subnet

#### Route Table:
    0.0.0.0/0 → Internet Gateway (IGW)

---

### 2.3 Configure Private Subnet

#### Route Table:
    0.0.0.0/0 → NAT Gateway

---

### 2.4 Flow of Traffic

- Private EC2 → NAT Gateway → Internet  
- Response → NAT Gateway → Private EC2  

#### Key Point:
- No inbound internet access to private instances  

---

### 3. Alternative: NAT Instance

- EC2 instance acting as NAT  
- Requires:
  - Disable source/destination check  
  - Manual scaling and maintenance  

#### Limitation:
- Less reliable and scalable than NAT Gateway  

---

### 4. Security Considerations

- Private instances:
  - No public IP  
- Security Groups:
  - Allow outbound traffic  
- NAT Gateway:
  - Only allows outbound initiated connections  

---

### 5. Key Takeaways

- Private subnets cannot access internet directly  
- NAT Gateway enables secure outbound access  
- NAT Gateway must be placed in public subnet  
- Route tables control traffic flow  

---

### 6. Interview-Ready Summary

“To allow internet access for instances in a private subnet, I would use a NAT Gateway. I would place the NAT Gateway in a public subnet with an internet gateway attached. Then, I would update the private subnet’s route table to route outbound traffic (0.0.0.0/0) to the NAT Gateway. This allows instances in the private subnet to access the internet securely for tasks like software updates, without exposing them to inbound internet traffic.”

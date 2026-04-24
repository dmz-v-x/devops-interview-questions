### Question  
You have been assigned to design a VPC architecture for a 2-tier application. The application needs to be highly available and scalable. How would you design the VPC architecture?

---

### 1. Overview

A **2-tier architecture** typically consists of:
- Web/Application Tier  
- Database Tier (optional extension)  

For high availability and scalability, the design must:
- Span multiple Availability Zones (AZs)  
- Use load balancing and auto scaling  
- Isolate resources using public and private subnets  

---

### 2. VPC Design

---

### 2.1 Create a VPC

- Define a VPC with a CIDR block (e.g., `10.0.0.0/16`)  
- Provides an isolated networking environment  

---

### 2.2 Subnet Design

Create two types of subnets across multiple AZs:

#### Public Subnets
- Used for:
  - Load Balancers (ALB/NLB)  
- Internet accessible  
- Example:
  - AZ1 → Public Subnet  
  - AZ2 → Public Subnet  

#### Private Subnets
- Used for:
  - Application servers (EC2)  
- No direct internet access  
- Example:
  - AZ1 → Private Subnet  
  - AZ2 → Private Subnet  

---

### 2.3 Internet Gateway (IGW)

- Attach IGW to VPC  
- Enables internet access for public subnets  

---

### 2.4 Route Tables

#### Public Subnet Route Table:
    0.0.0.0/0 → Internet Gateway

#### Private Subnet Route Table (optional):
    0.0.0.0/0 → NAT Gateway

---

### 2.5 NAT Gateway

- Placed in a public subnet  
- Allows private instances to access the internet  
- Prevents inbound internet access  

---

### 3. High Availability Design

---

### 3.1 Multi-AZ Deployment

- Deploy resources across at least 2 AZs  
- Ensures fault tolerance  

---

### 3.2 Load Balancer

- Use Application Load Balancer (ALB) in public subnets  
- Distributes traffic across instances in private subnets  

---

### 3.3 Auto Scaling Group

- Place EC2 instances in private subnets  
- Configure:
  - Minimum instances  
  - Maximum instances  
  - Scaling policies (CPU, memory, etc.)  

---

### 4. Security Design

---

### 4.1 Security Groups

- ALB:
  - Allow HTTP/HTTPS from internet  

- EC2:
  - Allow traffic only from ALB  

---

### 4.2 Network ACLs (Optional)

- Additional subnet-level security  

---

### 5. Optional Enhancements

- Add RDS in private subnets for database tier  
- Use Multi-AZ RDS for high availability  
- Enable VPC endpoints for private AWS access  
- Use WAF and Shield for application protection  

---

### 6. Key Takeaways

- Separate public and private subnets  
- Use ALB for traffic distribution  
- Deploy across multiple AZs  
- Use Auto Scaling for scalability  
- Secure communication using security groups  

---

### 7. Interview-Ready Summary

“For a highly available and scalable 2-tier application, I would design a VPC with public and private subnets across multiple availability zones. The public subnets would host load balancers, while private subnets would host application servers. I would use an internet gateway for public access and a NAT gateway for outbound access from private instances. To ensure scalability and availability, I would implement an Application Load Balancer and Auto Scaling Groups. Security groups would restrict access so only the load balancer communicates with application servers.”

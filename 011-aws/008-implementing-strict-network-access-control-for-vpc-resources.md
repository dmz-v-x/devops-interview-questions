### Question  
You want to implement strict network access control for your VPC resources. How would you achieve this?

---

### 1. Overview

To implement strict network access control in a VPC, we use a combination of:

- **Network ACLs (NACLs)** → subnet-level control (stateless)  
- **Security Groups (SGs)** → instance-level control (stateful)  

This layered approach provides **defense-in-depth security**.

---

### 2. Network ACLs (Primary Control)

---

### 2.1 What are NACLs?

- Operate at **subnet level**  
- **Stateless** (must allow both inbound and outbound explicitly)  
- Evaluate rules in **order (lowest number first)**  

---

### 2.2 Key Features

- Allow/Deny rules  
- Control:
  - Source/Destination IP  
  - Ports  
  - Protocols  

---

### 2.3 Example Rules

#### Inbound:
- Allow HTTP:
    ALLOW 80 from 0.0.0.0/0  

- Deny all else:
    DENY ALL  

#### Outbound:
- Allow response traffic:
    ALLOW ephemeral ports (1024–65535)  

---

### 3. Security Groups (Additional Layer)

---

### 3.1 What are Security Groups?

- Operate at **instance level**  
- **Stateful** (response traffic automatically allowed)  

---

### 3.2 Use Case

- Allow only required ports:
  - SSH (22)  
  - HTTP (80)  
  - HTTPS (443)  

- Restrict access by:
  - IP range  
  - Other security groups  

---

### 4. Combined Approach

| Layer           | Scope        | Type      | Purpose                        |
|----------------|-------------|-----------|--------------------------------|
| NACL           | Subnet      | Stateless | Broad network filtering        |
| Security Group | Instance    | Stateful  | Fine-grained access control    |

---

### 5. Additional Enhancements

- Use **VPC Flow Logs** for monitoring traffic  
- Implement **AWS WAF** for application-level filtering  
- Use **Private Subnets** for sensitive resources  
- Restrict outbound traffic where possible  

---

### 6. Key Takeaways

- NACLs provide strict subnet-level control  
- Security Groups provide instance-level filtering  
- Use both together for strong security  
- Always follow least privilege principle  

---

### 7. Interview-Ready Summary

“To implement strict network access control in a VPC, I use Network ACLs and Security Groups together. NACLs provide subnet-level, stateless filtering where I can define explicit allow and deny rules based on IP, port, and protocol. Security Groups provide instance-level, stateful filtering for more granular control. By combining both, I achieve layered security and enforce strict access control across the VPC.”

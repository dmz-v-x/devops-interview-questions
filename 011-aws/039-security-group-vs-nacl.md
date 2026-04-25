### Question  
Explain the difference between Security Groups (SG) and Network ACLs (NACL) in AWS.

---

### Answer  

---

### 1. Basics — What They Are

- **Security Group (SG):**
  - Stateful virtual firewall  
  - Attached to **instances / ENIs**  
  - Controls traffic at **instance level**  

- **Network ACL (NACL):**
  - Stateless virtual firewall  
  - Attached to **subnets**  
  - Controls traffic at **subnet level**  

---

### 2. Stateful vs Stateless

- **Security Group (Stateful):**
  - If inbound traffic is allowed → response is automatically allowed  
  - No need to define return rules  

- **NACL (Stateless):**
  - Must allow traffic **both inbound and outbound explicitly**  
  - No automatic return traffic handling  

---

### 3. Rule Model

- **Security Group:**
  - Only **allow rules** (no deny)  
  - Default:
    - Deny all inbound  
    - Allow all outbound  
  - If any rule matches → traffic allowed  

- **NACL:**
  - Supports **allow and deny rules**  
  - Rules processed in order:
    - Lowest number → highest  
    - First match wins  

  - Default behavior:
    - Default NACL → allows all  
    - Custom NACL → denies all  

---

### 4. Scope & Association

- **Security Group:**
  - Attached to:
    - Instance / ENI  
  - Multiple SGs can be attached  

- **NACL:**
  - Attached to:
    - Subnet  
  - One NACL per subnet  

---

### 5. Use Cases

- **Security Groups (Primary Use):**
  - Instance-level access control  
  - Fine-grained permissions  

  - Example:
    - Allow HTTP/HTTPS from ALB to EC2  

---

- **NACLs (Secondary Layer):**
  - Subnet-level protection  
  - Coarse-grained filtering  

  - Example:
    - Block malicious IP ranges  

---

### 6. Example Scenario

- Web application:

  - **Security Group:**
    - Allow:
      - 443 from internet → EC2  
      - 3306 from EC2 → RDS  

  - **NACL:**
    - Deny:
      - Known malicious IP ranges  

- Insight:
  - SG → controls app-level access  
  - NACL → adds extra security layer  

---

### 7. Quick Comparison Table

| Feature          | Security Group (SG)          | Network ACL (NACL)                   |
|------------------|-----------------------------|--------------------------------------|
| **Level**        | Instance / ENI              | Subnet                               |
| **Statefulness** | Stateful                    | Stateless                            |
| **Rules**        | Allow only                  | Allow + Deny                         |
| **Default**      | Deny inbound, allow outbound| Default: allow all; Custom: deny all |
| **Evaluation**   | All rules applied           | First match (low → high)             |
| **Common Use**   | Instance-level firewall     | Subnet-level filtering               |
| **Flexibility**  | Multiple SGs per ENI        | One NACL per subnet                  |

---

### 8. Key Takeaways

- Security Groups:
  - Primary and most used  
  - Fine-grained control  

- NACLs:
  - Secondary security layer  
  - Used for broader restrictions  

---

### 9. Interview-Ready Summary

“Security Groups are stateful firewalls applied at the instance level, allowing only specified traffic and automatically permitting return traffic. Network ACLs are stateless firewalls applied at the subnet level, requiring explicit rules for both inbound and outbound traffic. In practice, Security Groups are used for fine-grained access control, while NACLs provide an additional layer of subnet-level security.”

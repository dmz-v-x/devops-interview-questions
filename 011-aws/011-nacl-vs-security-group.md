### Question  
What is the difference between NACL and Security Groups? Explain with a use case.

---

### 1. Overview

In AWS VPC, both **Network ACLs (NACLs)** and **Security Groups (SGs)** are used to control traffic, but they operate at different levels and behave differently.

---

### 2. Key Differences

| Feature              | NACL (Network ACL)                  | Security Group                        |
|---------------------|------------------------------------|--------------------------------------|
| Level               | Subnet level                       | Instance level                        |
| Type                | Stateless                          | Stateful                              |
| Rules               | Allow & Deny                       | Allow only                            |
| Rule Evaluation     | In order (numbered rules)          | All rules evaluated together          |
| Return Traffic      | Must be explicitly allowed         | Automatically allowed                 |
| Scope               | Entire subnet                      | Specific EC2 instance                 |

---

### 3. NACL (Network ACL)

#### Characteristics:
- Applied at **subnet boundary**  
- Stateless → must allow both inbound & outbound traffic  
- Supports **allow and deny rules**  
- Rules are processed in **order (priority-based)**  

---

### 4. Security Groups

#### Characteristics:
- Applied at **instance level**  
- Stateful → return traffic automatically allowed  
- Supports **allow rules only**  
- Easier to manage  

---

### 5. Use Case Example

---

### Scenario: Secure Web Application Architecture

#### Requirement:
- Allow public access to web servers  
- Restrict backend/database access  
- Add an extra security layer  

---

### Step 1: Use NACL (Subnet-Level Security)

- Apply NACL on subnet:
  - Allow HTTP/HTTPS (80, 443) from internet  
  - Deny all other unwanted traffic  

#### Purpose:
- First layer of defense at network boundary  

---

### Step 2: Use Security Groups (Instance-Level Security)

- Web Server SG:
  - Allow HTTP/HTTPS from internet  

- App Server SG:
  - Allow traffic only from Web Server SG  

- Database SG:
  - Allow traffic only from App Server SG  

#### Purpose:
- Fine-grained access control between services  

---

### 6. Defense-in-Depth Strategy

| Layer            | Tool            | Purpose                         |
|-----------------|-----------------|---------------------------------|
| Network Layer   | NACL            | Broad traffic filtering         |
| Instance Layer  | Security Group  | Granular access control         |

---

### 7. Key Takeaways

- NACL = subnet-level, stateless, supports deny  
- Security Group = instance-level, stateful, allow-only  
- Use both together for strong security  

---

### 8. Interview-Ready Summary

“NACLs and Security Groups are both used for controlling network traffic in AWS VPC. NACLs operate at the subnet level and are stateless, meaning you must explicitly allow inbound and outbound traffic, and they support both allow and deny rules. Security Groups operate at the instance level and are stateful, meaning return traffic is automatically allowed and they only support allow rules. In practice, I use NACLs for coarse-grained filtering at the subnet level and Security Groups for fine-grained control at the instance level, achieving a defense-in-depth security model.”

### Question  
Your organization has a VPC with multiple subnets. You want to restrict outbound internet access for resources in one subnet, but allow outbound internet access for resources in another subnet. How would you achieve this?

---

### 1. Overview

In AWS VPC, **internet access is controlled primarily through route tables**.  
By configuring different route tables for different subnets, we can control outbound access.

---

### 2. Key Concept

- Internet access requires:
  - Route to `0.0.0.0/0`  
  - Target → Internet Gateway (IGW) or NAT Gateway  

- Removing or modifying this route **blocks internet access**

---

### 3. Solution Design

---

### 3.1 Subnet with Internet Access (Public or Private via NAT)

#### Route Table Configuration:
    0.0.0.0/0 → Internet Gateway (for public subnet)

OR (for private subnet with controlled outbound):
    0.0.0.0/0 → NAT Gateway

#### Result:
- Instances can access the internet  

---

### 3.2 Subnet WITHOUT Internet Access

#### Route Table Configuration:
- Remove default route:
    0.0.0.0/0

OR do not define any internet route

#### Result:
- No outbound internet connectivity  
- Instances can only communicate within VPC  

---

### 4. Optional Enhancements

---

### 4.1 Use NAT Gateway for Controlled Access

- Allow outbound internet  
- Block inbound connections  
- Best for private subnets needing updates  

---

### 4.2 Use Security Groups / NACLs (Additional Control)

- Security Groups:
  - Restrict outbound rules  

- NACLs:
  - Block internet traffic at subnet level  

---

### 5. Example Scenario

| Subnet Type        | Route Table                          | Internet Access |
|-------------------|--------------------------------------|-----------------|
| Public Subnet     | `0.0.0.0/0 → IGW`                    | Yes             |
| Private Subnet A  | `0.0.0.0/0 → NAT Gateway`            | Yes (Outbound)  |
| Private Subnet B  | No `0.0.0.0/0` route                 | No              |

---

### 6. Key Takeaways

- Route tables control internet access  
- Removing default route blocks outbound traffic  
- NAT Gateway allows controlled outbound access  
- Security Groups and NACLs provide additional restrictions  

---

### 7. Interview-Ready Summary

“To control outbound internet access in a VPC, I would use route tables. For the subnet that should not have internet access, I would remove the default route (0.0.0.0/0) pointing to the internet gateway. For the subnet that requires internet access, I would keep the default route pointing to the internet gateway or use a NAT gateway for private subnets. This approach ensures controlled and secure network access based on subnet requirements.”

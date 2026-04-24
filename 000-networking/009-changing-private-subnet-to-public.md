### Question  
You accidentally created a private subnet instead of a public subnet. How would you fix it?

---

### Answer  

A subnet becomes **public** when:
- It has a route to an **Internet Gateway (IGW)**  
- Instances can have **public IPs**  

To convert a private subnet into a public subnet, follow these steps:

---

### 1. Update the Route Table

- Go to:
  - VPC → Route Tables  

- Identify the route table associated with the subnet  

- Add a route:

```
Destination: 0.0.0.0/0
Target: igw-xxxxxxxx   # Internet Gateway ID
```

---

### 2. Associate the Correct Route Table

- In Route Tables:
  - Select the updated route table  

- Go to:
  - Subnet Associations tab  

- Ensure your subnet is associated with this route table  

---

### 3. Enable Auto-Assign Public IP

- Go to:
  - VPC → Subnets → Select your subnet  

- Click:
  - Actions → Modify auto-assign IP settings  

- Enable:
```
Auto-assign IPv4 public IP
```

---

### 4. Assign Public IP to Existing Instances

If EC2 instances already exist without public IP:

---

#### Option 1: Assign Elastic IP

- Go to:
  - EC2 → Elastic IPs  

- Allocate new Elastic IP  
- Associate it with the instance  

---

#### Option 2: Attach to Network Interface

- Go to:
  - EC2 → Network Interfaces  

- Attach Elastic IP to primary interface  

---

### 5. Ensure Internet Gateway is Attached

- Go to:
  - VPC → Internet Gateways  

- Verify:
  - IGW is attached to the same VPC  

---

### 6. Final Architecture Check

Ensure:

```
Subnet → Route Table → IGW → Internet
```

---

### 7. Key Takeaways

- Public subnet = route to IGW + public IP  
- Route table is the deciding factor  
- Existing instances may need Elastic IP  
- IGW must be attached to VPC  

---

### 8. Interview-Ready Summary

“To convert a private subnet into a public subnet, I update its route table to include a default route to an Internet Gateway, ensure the subnet is associated with that route table, enable auto-assign public IPs, and attach Elastic IPs to existing instances if needed. I also verify that the Internet Gateway is attached to the VPC.”

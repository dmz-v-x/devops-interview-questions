### Question  
How to enable internet access to applications deployed in a private subnet of a VPC?

---

### Answer  

---

### 1. Understanding the Problem

- Private subnet:
  - No direct internet access  
  - No route to Internet Gateway (IGW)  

- Requirement:
  - Allow **secure outbound internet access**  
  - Without exposing instances publicly  

---

### 2. Public vs Private Subnet Routing

- **Public Subnet Route Table:**

```text
0.0.0.0/0 → Internet Gateway (IGW)
```

- **Private Subnet:**
  - No internet route by default  

---

### 3. Solution: Use NAT Gateway

- NAT Gateway enables:
  - **Outbound internet access** for private instances  
  - While keeping them private  

---

### 4. Steps to Enable Internet Access

---

### Step 1: Create NAT Gateway

- Place NAT Gateway in:
  - **Public Subnet**  

- Attach:
  - **Elastic IP (EIP)**  

---

### Step 2: Update Route Table (Private Subnet)

```text
Destination: 0.0.0.0/0 → NAT Gateway
```

- This ensures:
  - All outbound traffic goes via NAT  

---

### Step 3: Ensure Public Subnet Has IGW

```text
0.0.0.0/0 → Internet Gateway
```

- Required for NAT to access internet  

---

### 5. Traffic Flow

1. Private instance sends request (e.g., to Google)  
2. Request goes to NAT Gateway  
3. NAT:
   - Replaces private IP with its public IP  
4. Request goes to internet  
5. Response returns to NAT  
6. NAT forwards it back to private instance  

---

### 6. Security Benefits

- No direct inbound access  
- Private IP remains hidden  
- Controlled outbound access  

---

### 7. Key Takeaways

- Private subnet:
  - Cannot access internet directly  

- NAT Gateway:
  - Enables secure outbound access  

- Routing is the key:
  - Private subnet → NAT  
  - NAT → IGW  

---

### 8. Interview-Ready Summary

“To enable internet access for applications in a private subnet, I would use a NAT Gateway placed in a public subnet with an Elastic IP. Then I would update the private subnet’s route table to route traffic (0.0.0.0/0) to the NAT Gateway. This allows instances to access the internet securely while preventing any inbound connections, keeping the system protected.”

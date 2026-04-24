### Question  
What is a subnet mask? How does subnetting work?

---

### Answer  

---

### 1. What is a Subnet Mask?

- A **subnet mask** is used to divide an IP address into:
  - **Network portion**  
  - **Host portion**  

---

#### Purpose:

- Identifies:
  - Which part of the IP belongs to the network  
  - Which part identifies a device (host)  

---

### 2. Example

IP Address:
```
192.168.1.10
```

Subnet Mask:
```
255.255.255.0
```

---

#### Breakdown:

- Network part:
```
192.168.1
```

- Host part:
```
10
```

---

#### Meaning:

- Device belongs to network:
```
192.168.1.0
```

---

### 3. How Subnetting Works

- **Subnetting** = dividing a large network into smaller sub-networks  

---

#### Why subnet?

- Better organization  
- Improved security  
- Efficient IP usage  
- Reduced network congestion  

---

#### Concept:

- Borrow bits from host portion  
- Create multiple smaller networks  

---

### 4. CIDR Notation

- Instead of full mask, we use **CIDR**  

Example:

```
192.168.1.10/24
```

---

#### Meaning:

- `/24` → first 24 bits = network  
- Equivalent to:
```
255.255.255.0
```

---

### 5. Simple Visualization

```
IP Address:   192.168.1.10
Subnet Mask:  255.255.255.0

Network → 192.168.1
Host    → .10
```

---

### 6. Key Takeaways

- Subnet mask splits IP into:
  - Network + Host  
- Subnetting creates smaller networks  
- CIDR simplifies subnet representation  

---

### 7. Interview-Ready Summary

“A subnet mask is used to divide an IP address into network and host portions, helping identify which network a device belongs to. Subnetting is the process of splitting a large network into smaller subnets for better management, security, and efficient IP usage. CIDR notation like /24 represents the subnet mask in a simplified form.”

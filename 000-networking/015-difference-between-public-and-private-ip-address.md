### Question  
Explain the difference between a public and private IP address.

---

### Answer  

---

### 1. Public IP Address

- A **public IP address** is assigned by an **ISP or cloud provider**  
- It is:
  - **Globally unique**  
  - **Accessible over the internet**  

---

#### Characteristics:

- Used for:
  - Websites  
  - Public servers  
- Reachable from anywhere on the internet  

---

#### Example:

```
8.8.8.8   (Google DNS)
203.0.113.1
```

---

### 2. Private IP Address

- A **private IP address** is used within a **local network (LAN)**  
- It is:
  - **Not accessible directly from the internet**  
  - Used for internal communication  

---

#### Reserved Private Ranges:

```
10.0.0.0 – 10.255.255.255
172.16.0.0 – 172.31.255.255
192.168.0.0 – 192.168.255.255
```

---

#### Example:

```
192.168.1.10
10.0.0.5
```

---

### 3. Key Differences

| Feature         | Public IP                    | Private IP                              |
| --------------- | ---------------------------- | --------------------------------------- |
| **Scope**       | Global (Internet-wide)       | Local (LAN only)                        |
| **Uniqueness**  | Must be unique globally      | Unique only within network              |
| **Assigned by** | ISP / Cloud provider         | Router / DHCP / manual                  |
| **Access**      | Accessible from internet     | Not accessible without NAT              |
| **Example**     | `203.0.113.1`                | `192.168.1.10`                          |

---

### 4. How They Work Together

- Devices in a local network use **private IPs**  
- Router uses **NAT (Network Address Translation)** to:
  - Convert private IP → public IP  

---

#### Flow:

```
Private IP → Router (NAT) → Public IP → Internet
```

---

### 5. Key Takeaways

- Public IP → internet-facing  
- Private IP → internal communication  
- NAT bridges the two  

---

### 6. Interview-Ready Summary

“A public IP address is globally unique and accessible over the internet, typically assigned by an ISP or cloud provider. A private IP address is used within a local network and is not directly reachable from the internet. Private IPs rely on NAT to communicate with external networks.”

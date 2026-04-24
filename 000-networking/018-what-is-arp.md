### Question  
What is ARP?

---

### Answer  

---

### 1. What is ARP?

- ARP stands for **Address Resolution Protocol**  
- It is used to map:
  - **IP address → MAC address**  

---

#### Purpose:

- Enables communication within a **local network (LAN)**  
- Devices need MAC addresses to send data at Layer 2  

---

### 2. Why ARP is Needed

- Communication flow:
  - IP (Layer 3) → Routing  
  - MAC (Layer 2) → Delivery  

👉 ARP bridges this gap  

---

### 3. How ARP Works (Step-by-Step)

---

#### Step 1: Need to Send Data

- Your system wants to send data to:
```
192.168.1.10
```

---

#### Step 2: Check ARP Cache

- Looks in local cache for MAC address  

---

#### Step 3: ARP Request (Broadcast)

- If not found, sends request:
```
"Who has 192.168.1.10?"
```

---

#### Step 4: ARP Reply

- Target device responds:
```
"192.168.1.10 is at AA:BB:CC:DD:EE:FF"
```

---

#### Step 5: Cache Storage

- Stores mapping in ARP table  

---

#### Step 6: Data Transmission

- Uses MAC address to send packet  

---

### 4. ARP Cache

- Temporary storage of IP → MAC mappings  

---

#### View ARP Table:

```bash
arp -a
```

or

```bash
ip neigh
```

---

### 5. Key Takeaways

- ARP maps IP to MAC  
- Works only within local network  
- Uses broadcast + reply mechanism  
- Improves performance via caching  

---

### 6. Real-World Analogy

- IP address → Person’s name  
- MAC address → House address  

ARP = Asking:
“Where does this person live?”  

---

### 7. Interview-Ready Summary

“ARP, or Address Resolution Protocol, is used to map an IP address to a MAC address within a local network. When a device wants to communicate with another device, it broadcasts an ARP request to find the MAC address corresponding to the target IP. The response is cached and used for efficient communication.”

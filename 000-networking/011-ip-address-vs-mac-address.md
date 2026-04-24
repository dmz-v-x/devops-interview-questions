### Question  
What is an IP address? How is it different from a MAC address?

---

### Answer  

---

### 1. What is an IP Address?

- An **IP (Internet Protocol) address** is a **logical address** assigned to a device  
- It identifies the device’s **location on a network**  
- Used for **routing data across networks (internet)**  

---

#### Types of IP Addresses:

- **IPv4**:
```
192.168.1.1
```

- **IPv6**:
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

---

### 2. What is a MAC Address?

- A **MAC (Media Access Control) address** is a **physical hardware address**  
- Assigned to the **network interface card (NIC)** by the manufacturer  
- Used for communication **within a local network (LAN)**  

---

#### Example:

```
00:1A:2B:3C:4D:5E
```

---

### 3. Key Differences

| Feature        | IP Address                                    | MAC Address                              |
| -------------- | --------------------------------------------- | ---------------------------------------- |
| **Type**       | Logical address                               | Physical (hardware) address              |
| **Layer**      | Network Layer (Layer 3)                       | Data Link Layer (Layer 2)                |
| **Permanence** | Can change (dynamic or static)                | Permanent (assigned by manufacturer)     |
| **Purpose**    | Identifies device across networks             | Identifies device within local network   |
| **Example**    | `192.168.1.10`                                | `00:1A:2B:3C:4D:5E`                      |

---

### 4. How They Work Together

- IP address → Used to **route data across networks**  
- MAC address → Used to **deliver data within local network**  

---

#### Flow Example:

```
Client → Router (IP routing) → Local Network → Device (MAC delivery)
```

---

### 5. Real-World Analogy

- IP Address → Like a **home address (city, street)**  
- MAC Address → Like a **person’s identity inside the house**  

---

### 6. Key Takeaways

- IP = logical + routing  
- MAC = physical + local delivery  
- Both are essential for communication  

---

### 7. Interview-Ready Summary

“An IP address is a logical address used to identify a device across networks and enable routing, while a MAC address is a physical hardware address used to identify a device within a local network. IP addresses can change, but MAC addresses are usually fixed. Both work together to ensure data reaches the correct destination.”

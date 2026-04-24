### Question  
What is the role of DNS in networking? How do you check DNS resolution in Linux?

---

### Answer  

---

### 1. Role of DNS in Networking

- DNS (Domain Name System) acts like the **phonebook of the internet**  
- It translates:
  - **Domain names → IP addresses**  

---

#### Example:

```
www.google.com → 142.250.190.132
```

---

### 2. Why DNS is Important

| Function                    | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| **Name-to-IP resolution**   | Converts domain names to IP addresses                 |
| **Simplifies networking**   | Easier to remember names than numbers                 |
| **Enables scalability**     | IPs can change without affecting users                |
| **Supports load balancing** | Returns different IPs to distribute traffic           |

---

### 3. How to Check DNS Resolution in Linux

---

### 3.1 Using `dig` (Detailed)

```bash
dig google.com
```

#### Features:

- Detailed DNS response  
- Shows:
  - Answer section  
  - DNS server used  
  - Query time  

---

### 3.2 Using `nslookup` (Simple)

```bash
nslookup google.com
```

#### Features:

- Quick resolution  
- Easy to read output  

---

### 3.3 Using `host` (Fastest)

```bash
host google.com
```

#### Features:

- Minimal output  
- Fast lookup  

---

### 4. DNS Configuration Files in Linux

---

#### `/etc/resolv.conf`

- Defines DNS servers:

```
nameserver 8.8.8.8
```

---

#### `/etc/hosts`

- Local hostname mappings  
- Checked **before DNS**

---

### 5. Key Takeaways

- DNS = domain → IP translation  
- Essential for internet usability  
- Use:
  - `dig` → detailed debugging  
  - `nslookup` → simple lookup  
  - `host` → quick check  

---

### 6. Interview-Ready Summary

“DNS translates domain names into IP addresses, enabling users to access services without remembering numeric addresses. To check DNS resolution in Linux, I use tools like dig for detailed output, nslookup for simple resolution, and host for quick lookups. I also verify DNS configuration in /etc/resolv.conf and check /etc/hosts for local overrides.”

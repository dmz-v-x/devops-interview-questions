### Question  
What command do you use to check network interfaces in Linux?

---

### Answer  

---

### 1. Using `ip a` (Recommended)

```bash
ip a
```

or

```bash
ip address
```

#### What it shows:
- All network interfaces  
- IP addresses (IPv4 & IPv6)  
- Interface status (UP/DOWN)  

---

### 2. Using `ip link`

```bash
ip link
```

#### What it shows:
- Interface names  
- MAC addresses  
- Status (UP/DOWN)  

👉 Does **not** show IP addresses  

---

### 3. Using `ifconfig` (Legacy)

```bash
ifconfig
```

#### Notes:
- Older command (from `net-tools`)  
- Deprecated in modern Linux systems  
- Still used in some environments  

---

### 4. Key Takeaways

- `ip a` → most commonly used (modern)  
- `ip link` → interface status only  
- `ifconfig` → legacy tool  

---

### 5. Interview-Ready Summary

“To check network interfaces in Linux, I use the ip a command, which shows all interfaces along with their IP addresses and status. Alternatively, ip link can be used to view interface status, and ifconfig is an older, deprecated command still available in some systems.”

### Question  
What is the difference between `ifconfig` and `ip` commands?

---

### Answer  

Both `ifconfig` and `ip` are used to **view and configure network interfaces**, but they differ in capability and modern usage.

---

### 1. Overview

- `ifconfig`:
  - Older tool  
  - Part of **net-tools** package  
  - **Deprecated** in modern Linux  

- `ip`:
  - Newer tool  
  - Part of **iproute2** suite  
  - **Standard in modern Linux systems**  

---

### 2. Key Differences

| Feature        | `ifconfig`                     | `ip`                                 |
| -------------- | ------------------------------ | ------------------------------------ |
| Status         | Deprecated                     | Actively maintained                  |
| Package        | net-tools                      | iproute2                             |
| Functionality  | Basic                          | Advanced                             |
| IPv6 Support   | Limited                        | Full                                 |
| Flexibility    | Limited                        | High                                 |
| Use Today      | Not recommended                | Recommended                          |

---

### 3. Common Tasks Comparison

| Task                    | `ifconfig` Example            | `ip` Equivalent                         |
| ----------------------- | ----------------------------- | --------------------------------------- |
| View interfaces         | `ifconfig`                    | `ip addr` or `ip a`                     |
| Bring interface up/down | `ifconfig eth0 up`            | `ip link set eth0 up`                   |
| Assign IP address       | `ifconfig eth0 192.168.1.100` | `ip addr add 192.168.1.100/24 dev eth0` |
| Remove IP address       | *(not supported directly)*    | `ip addr del 192.168.1.100/24 dev eth0` |
| View routing table      | `route -n` or `netstat -rn`   | `ip route`                              |

---

### 4. Why `ip` is Preferred

- Supports:
  - IPv4 and IPv6  
  - Multiple IPs per interface  
  - Routing, bridges, VLANs, tunnels  
- Consistent and structured syntax  
- Actively maintained  

---

### 5. Key Takeaways

- `ifconfig` → legacy tool  
- `ip` → modern, powerful replacement  
- Always prefer `ip` in production systems  

---

### 6. Interview-Ready Summary

“ifconfig is an older networking tool from the net-tools package and is now deprecated, while ip is the modern replacement from the iproute2 suite. The ip command provides more advanced features, better IPv6 support, and a consistent syntax, making it the preferred tool in modern Linux systems.”

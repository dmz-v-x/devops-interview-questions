### Question  
What is the difference between `ifconfig` and `ip` command?

---

### Answer  

---

### 1. `ifconfig` Command

#### Purpose

- Used to **view and configure network interfaces**  
- Legacy tool; part of **net-tools package**  
- Now considered **deprecated** in most modern Linux distributions  

---

#### Common Uses

| Use Case                | Command Example                                          |
| ----------------------- | -------------------------------------------------------- |
| View all interfaces     | `ifconfig -a`                                            |
| Assign IP to interface  | `sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0` |
| Bring interface up/down | `sudo ifconfig eth0 up` / `sudo ifconfig eth0 down`      |
| View MAC address        | `ifconfig eth0` (look for `HWaddr`)                      |

---

#### Characteristics

- Simple and easy for basic tasks  
- Limited functionality compared to modern tools  
- Does not support advanced features like:
  - Policy routing  
  - Namespaces  
  - Advanced networking  

---

### 2. `ip` Command

#### Purpose

- Part of **iproute2 package**  
- Modern replacement for `ifconfig`  
- Manages:
  - Network interfaces  
  - IP addresses  
  - Routes  
  - Tunnels  
  - Links  

---

#### Common Uses

| Use Case                | Command Example                                           |
| ----------------------- | --------------------------------------------------------- |
| Show all interfaces     | `ip addr show` or `ip a`                                  |
| Assign IP address       | `sudo ip addr add 192.168.1.100/24 dev eth0`              |
| Delete IP address       | `sudo ip addr del 192.168.1.100/24 dev eth0`              |
| Bring interface up/down | `sudo ip link set eth0 up` / `sudo ip link set eth0 down` |
| Show routing table      | `ip route show` or `ip r`                                 |
| View MAC address        | `ip link show eth0`                                       |

---

#### Advantages

- Full support for **IPv4 and IPv6**  
- Allows **multiple IP addresses per interface**  
- Supports advanced networking:
  - VLANs  
  - Tunnels  
  - Bridges  
- Preferred in modern Linux distributions  

---

### 3. Key Differences

| Feature                    | `ifconfig`                       | `ip`                                                          |
| -------------------------- | -------------------------------- | ------------------------------------------------------------- |
| Status                     | Legacy/deprecated                | Modern replacement                                            |
| Package                    | `net-tools`                      | `iproute2`                                                    |
| IPv6 Support               | Limited                          | Full                                                          |
| Functionality              | Basic (interfaces and addresses) | Advanced (interfaces, addresses, routes, tunnels, namespaces) |
| Syntax                     | Simple, short commands           | Verbose but consistent structure                              |
| Multiple IPs per interface | Harder to manage                 | Easy                                                          |
| Use in modern Linux        | Not recommended                  | Recommended                                                   |

---

### 4. Real-World Example

#### Scenario: Add a new IP to an interface

```bash
# Using ifconfig (deprecated)
sudo ifconfig eth0:1 192.168.1.50 netmask 255.255.255.0 up

# Using ip (modern)
sudo ip addr add 192.168.1.50/24 dev eth0
sudo ip link set eth0 up
```

---

#### Scenario: Check the interface status

```bash
ifconfig
ip addr show
```

- `ip` provides more structured and detailed output  

---

### 5. Tricky Interview Questions

---

#### Q: Why is `ifconfig` deprecated?  
**A:**  
- It does not support modern networking features like:
  - Multiple IPs per interface  
  - Namespaces  
  - Policy routing  
  - Advanced metrics  
- `ip` is more versatile and actively maintained  

---

#### Q: How do you display all IPv6 addresses assigned to an interface?  
**A:**

```bash
ip -6 addr show dev eth0
```

---

#### Q: How do you bring an interface down using `ip`?  
**A:**

```bash
sudo ip link set eth0 down
```

---

#### Q: How do you check the default route?  
**A:**

```bash
ip route show default
```

---

### 6. Interview-Ready Summary

“`ifconfig` is a legacy networking tool used for basic interface configuration, but it is now deprecated. The `ip` command is its modern replacement, part of the iproute2 package, and provides advanced networking capabilities such as routing, multiple IP management, IPv6 support, and namespace handling. In modern Linux systems, `ip` is the recommended tool.”

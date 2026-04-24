### Question  
How do you assign an IP address to a network interface temporarily in Linux?

---

### Answer  

To assign an IP address **temporarily** (lost after reboot or interface restart), use the `ip` command.

---

### 1. Command

```bash
sudo ip addr add <IP_ADDRESS>/<SUBNET_MASK> dev <INTERFACE>
```

---

### 2. Example

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

- Assigns:
  - IP → `192.168.1.100`  
  - Subnet → `/24` (255.255.255.0)  
  - Interface → `eth0`  

---

### 3. Verify the Assignment

```bash
ip a
```

- Check if the IP is added to the interface  

---

### 4. Remove the IP (Optional)

```bash
sudo ip addr del 192.168.1.100/24 dev eth0
```

---

### 5. Important Notes

- This change is:
  - Temporary  
  - Lost after reboot or interface restart  

---

### 6. How to Make It Permanent

Depends on Linux distribution:

- `/etc/network/interfaces` (Debian/Ubuntu older systems)  
- Netplan (`/etc/netplan/*.yaml`)  
- NetworkManager (`nmcli`)  

---

### 7. Key Takeaways

- Use `ip addr add` for quick testing  
- Always verify using `ip a`  
- Not persistent across reboots  

---

### 8. Interview-Ready Summary

“To assign an IP address temporarily in Linux, I use the ip addr add command, specifying the IP, subnet, and interface. This change is not persistent and will be removed after a reboot. For permanent configuration, I modify network configuration files or use tools like Netplan or NetworkManager.”

### Question
Explain how to configure a static IP address in Linux.

### Answer

A **static IP address** is an IP address that is manually assigned to a system and remains constant, unlike a dynamic IP assigned by a DHCP server which may change over time.

Static IPs are commonly used for systems that must always be reachable at the same address.

Examples include:

- Web servers
- Database servers
- Mail servers
- Network devices such as routers, printers, and NAS systems

---

### Understanding Static vs Dynamic IP

| Type | Description |
|-----|-------------|
| Static IP | Manually configured and does not change |
| Dynamic IP (DHCP) | Automatically assigned by a DHCP server and may change |

---

### Methods to Configure a Static IP

The exact method depends on the Linux distribution and network management system used.

---

### Temporary Static IP Configuration (Using `ip` command)

You can configure a temporary static IP using the `ip` command. This change is **not persistent** and will be lost after a reboot.

Commands:

    sudo ip addr add 192.168.1.100/24 dev eth0
    sudo ip route add default via 192.168.1.1

Explanation:

- `192.168.1.100/24` → IP address and subnet mask
- `eth0` → network interface
- `192.168.1.1` → default gateway

Check the assigned IP:

    ip addr show eth0

Note: This configuration will reset after reboot.

---

### Permanent Static IP Configuration

To make the configuration persistent, you must edit network configuration files or use network management tools.

---

### Ubuntu / Debian (Using Netplan)

Modern Ubuntu systems use **Netplan** for network configuration.

Open the Netplan configuration file:

    sudo nano /etc/netplan/01-netcfg.yaml

Example configuration:

    network:
      version: 2
      ethernets:
        eth0:
          dhcp4: no
          addresses:
            - 192.168.1.100/24
          gateway4: 192.168.1.1
          nameservers:
            addresses: [8.8.8.8, 8.8.4.4]

Explanation:

- `dhcp4: no` disables DHCP
- `addresses` defines the static IP
- `gateway4` defines the default gateway
- `nameservers` sets DNS servers

Apply the configuration:

    sudo netplan apply

---

### RHEL / CentOS / Fedora (Network Configuration Files)

Older RHEL/CentOS systems use configuration files located in:

    /etc/sysconfig/network-scripts/

Edit the interface configuration file:

    sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0

Example configuration:

    DEVICE=eth0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.1.100
    NETMASK=255.255.255.0
    GATEWAY=192.168.1.1
    DNS1=8.8.8.8
    DNS2=8.8.4.4

Explanation:

- `BOOTPROTO=static` sets static configuration
- `ONBOOT=yes` ensures interface starts during boot
- `IPADDR`, `NETMASK`, `GATEWAY` configure networking
- `DNS1` and `DNS2` configure DNS servers

Restart networking:

    sudo systemctl restart network

or reload NetworkManager:

    sudo nmcli connection reload

---

### Configuring Static IP Using `nmcli` (NetworkManager CLI)

`nmcli` is a command-line tool used to manage NetworkManager connections.

Commands:

    sudo nmcli con mod "Wired connection 1" ipv4.addresses 192.168.1.100/24
    sudo nmcli con mod "Wired connection 1" ipv4.gateway 192.168.1.1
    sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8 8.8.4.4"
    sudo nmcli con mod "Wired connection 1" ipv4.method manual
    sudo nmcli con up "Wired connection 1"

Explanation:

- Sets IP address
- Configures gateway
- Defines DNS servers
- Changes method to manual
- Activates the connection

---

### Verifying the Configuration

After configuring a static IP, verify the network settings.

Check IP address:

    ip addr show eth0

Check routing table:

    ip route show

Check network connectivity:

    ping 8.8.8.8

Check DNS resolution:

    ping google.com

---

### Troubleshooting Common Issues

IP conflict  
Ensure no other device on the network uses the same IP address.

Incorrect gateway  
If the gateway is wrong, the system cannot communicate outside the local network.

DNS issues  
If you can ping an IP but not a domain name, verify DNS settings in:

    /etc/resolv.conf

Interface down  
Ensure the network interface is enabled:

    sudo ip link set eth0 up

---

### Interview / Tricky Questions

How can you configure a static IP without editing configuration files?

Use `nmcli` commands to modify the network configuration.

---

How do you verify DNS functionality after configuring a static IP?

    ping google.com

or

    dig google.com

---

How do you revert from static IP to DHCP?

Ubuntu / Debian (Netplan):

    dhcp4: yes

RHEL / CentOS:

    BOOTPROTO=dhcp

Using `nmcli`:

    sudo nmcli con mod "Wired connection 1" ipv4.method auto

---

What is the difference between temporary and permanent IP configuration?

Temporary configuration using:

    ip addr

is lost after reboot.

Permanent configuration using **Netplan, NetworkManager, or configuration files** persists across reboots.

---

### Interview Summary

A static IP in Linux can be configured temporarily using the `ip` command or permanently using tools such as **Netplan, NetworkManager (`nmcli`), or network configuration files**. Static IP addresses are essential for servers and network devices that require consistent connectivity.

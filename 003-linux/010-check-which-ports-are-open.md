### Question
How do you check which ports are open on a Linux system?

### Answer

In Linux, open ports indicate services that are listening for network connections. Administrators often check open ports to verify running services, troubleshoot connectivity issues, or perform security checks.

Several commands can be used to check open ports, including `netstat`, `ss`, `lsof`, `nmap`, and `fuser`.

---

### Using the `netstat` Command (Traditional Tool)

`netstat` displays network connections, listening ports, and routing information.

Basic command:

    netstat -tuln

Explanation of options:

| Option | Meaning |
|------|---------|
| `-t` | Show TCP ports |
| `-u` | Show UDP ports |
| `-l` | Show only listening ports |
| `-n` | Show numeric addresses and ports |

Example output:

    Proto Recv-Q Send-Q Local Address   Foreign Address   State
    tcp        0      0 0.0.0.0:22      0.0.0.0:*          LISTEN
    tcp6       0      0 :::80           :::*               LISTEN
    udp        0      0 0.0.0.0:68      0.0.0.0:*

This shows services listening on ports such as **SSH (22)** and **HTTP (80)**.

Note: `netstat` is considered an **older tool** and is gradually being replaced by `ss`.

---

### Using the `ss` Command (Modern Replacement)

`ss` is a faster and more modern tool for displaying socket statistics.

Basic command:

    ss -tuln

Options are similar to `netstat`.

To also display the process using each port:

    ss -tulnp

Explanation:

- `-p` shows the **PID and process name** associated with the port.

---

### Using the `lsof` Command

`lsof` lists open files, including network sockets.

Basic command:

    sudo lsof -i -P -n

Explanation:

| Option | Meaning |
|------|---------|
| `-i` | Show network files |
| `-P` | Display port numbers instead of service names |
| `-n` | Avoid DNS resolution |

Check a specific port:

    sudo lsof -i :22

This shows which process is using port **22**.

---

### Using the `nmap` Command

`nmap` is a network scanning tool used to detect open ports and services.

Example scan:

    sudo nmap -sT -O localhost

Explanation:

| Option | Meaning |
|------|---------|
| `-sT` | TCP connect scan |
| `-O` | Detect operating system |

Scan a specific port range:

    sudo nmap -p 20-100 localhost

---

### Using the `fuser` Command

`fuser` identifies which processes are using specific ports.

Example:

    sudo fuser 22/tcp

This returns the **PID of the process using port 22**.

---

### Summary of Commands

| Command | Purpose |
|-------|---------|
| `netstat -tuln` | Show listening TCP/UDP ports (traditional method) |
| `ss -tuln` | Modern and faster alternative to netstat |
| `ss -tulnp` | Show open ports with associated processes |
| `lsof -i -P -n` | Display all open network connections |
| `lsof -i :<port>` | Show process using a specific port |
| `nmap -p <range> localhost` | Scan ports on a system |
| `fuser <port>/tcp` | Identify PID using a specific port |

---

### Practical Example Workflow

Check all listening ports with processes:

    ss -tulnp

Check which process is using port 22:

    sudo lsof -i :22

Scan all ports on the local system:

    sudo nmap -p 1-65535 localhost

---

### Interview Summary

To check open ports in Linux, commonly used commands include `ss`, `netstat`, `lsof`, `nmap`, and `fuser`. Among these, `ss -tulnp` is the most widely recommended modern command because it quickly shows listening ports along with the processes using them.

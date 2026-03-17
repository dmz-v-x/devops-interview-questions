### Question  
How does this Shell Script check listening ports, and how does it work step by step?

---

### Answer  

### Complete Script  

    #!/bin/bash
    # Listening Port Check Script

    # Check for netstat/ss
    if command -v ss &> /dev/null; then
        ss -tuln
    elif command -v netstat &> /dev/null; then
        netstat -tuln
    else
        echo "Error: Neither ss nor netstat found!" >&2
        exit 1
    fi

---

### 1. Script Overview  

This script checks which ports are **currently listening** on the system by:

- Detecting available networking tools (`ss` or `netstat`)  
- Executing the appropriate command  
- Displaying open/listening ports  

---

### 2. Code Breakdown  

---

#### Shebang  

    #!/bin/bash

- Runs the script using the **Bash shell**

---

#### Check if `ss` Command Exists  

    if command -v ss &> /dev/null; then

- `command -v ss`:
  - Checks if `ss` is installed  
- `&> /dev/null`:
  - Suppresses output  

If found → runs:

    ss -tuln

---

#### Fallback to `netstat`  

    elif command -v netstat &> /dev/null; then

- If `ss` is not available, check for `netstat`  

If found → runs:

    netstat -tuln

---

#### Error Case  

    else
        echo "Error: Neither ss nor netstat found!" >&2
        exit 1
    fi

- If neither tool exists:
  - Print error to **stderr**  
  - Exit with failure  

---

### 3. Command Options Explained  

---

#### `ss -tuln`  

| Option | Meaning |
|---|---|
| `-t` | Show TCP ports |
| `-u` | Show UDP ports |
| `-l` | Show listening sockets |
| `-n` | Show numeric addresses (no DNS lookup) |

---

#### `netstat -tuln`  

Same meaning as above:

| Option | Meaning |
|---|---|
| `-t` | TCP |
| `-u` | UDP |
| `-l` | Listening |
| `-n` | Numeric |

---

### 4. Sample Output  

Example:

    tcp   LISTEN  0  128  0.0.0.0:22   0.0.0.0:*
    tcp   LISTEN  0  100  127.0.0.1:3000  0.0.0.0:*
    udp   UNCONN  0  0    0.0.0.0:68   0.0.0.0:*

Meaning:

- Port **22** → SSH server  
- Port **3000** → Local app  
- Port **68 (UDP)** → DHCP  

---

### 5. Execution Flow  

1. Script starts  
2. Checks if `ss` exists  
3. If yes → runs `ss -tuln`  
4. Else checks `netstat`  
5. If yes → runs `netstat -tuln`  
6. If neither → prints error and exits  

---

### 6. Real-World Use Cases  

---

Check running services:

    ss -tuln

---

Debug port conflicts:

    ss -tuln | grep 3000

---

Verify if server is listening on a port:

    ss -tuln | grep 80

---

Used in DevOps health checks and monitoring scripts  

---

---

### 7. Improvements / Best Practices  

---

#### Show Process Names  

    ss -tulnp

- Adds process information (requires sudo)

---

#### Filter Specific Port  

    ss -tuln | grep :8080

---

#### Use `lsof` Alternative  

    lsof -i :3000

---

#### Require Root for Full Info  

    sudo ss -tulnp

---

### 8. Tricky Interview Questions  

---

Why prefer `ss` over `netstat`?  

- Faster and more modern  
- Better performance on large systems  

---

What does `-n` do?  

- Avoids DNS lookup → faster output  

---

Difference between LISTEN and ESTABLISHED?  

| State | Meaning |
|---|---|
| LISTEN | Waiting for connections |
| ESTABLISHED | Active connection |

---

What is a socket?  

- Combination of IP + Port used for communication  

---

### Interview Summary  

This script checks listening ports by using `ss` (preferred) or `netstat` (fallback). It ensures compatibility across systems and helps identify open ports and active network services, which is essential for debugging and system monitoring.

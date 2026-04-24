### Question  
How do you test connectivity to a remote host?

---

### Answer  

To test connectivity to a remote host in Linux, you can use several tools depending on what level of connectivity you want to verify.

---

### 1. Using `ping` (Basic Connectivity)

```bash
ping <hostname or IP>
```

#### Example:

```bash
ping google.com
```

---

#### What it does:

- Sends ICMP echo requests  
- Checks:
  - Host reachability  
  - Response time (latency)  

---

### 2. Using `traceroute` (Path Analysis)

```bash
traceroute <hostname or IP>
```

---

#### What it does:

- Shows the path packets take  
- Identifies:
  - Network hops  
  - Where the connection is failing  

---

### 3. Using `curl` or `wget` (Application Layer)

```bash
curl http://example.com
```

or

```bash
wget http://example.com
```

---

#### What it does:

- Tests:
  - HTTP/HTTPS connectivity  
- Useful for:
  - Web services  
  - APIs  

---

### 4. Using `telnet` or `nc` (Port Connectivity)

```bash
telnet <host> <port>
```

or

```bash
nc -zv <host> <port>
```

---

#### What it does:

- Checks if a specific port is:
  - Open  
  - Reachable  

---

### 5. Key Takeaways

- `ping` → basic reachability  
- `traceroute` → network path  
- `curl/wget` → application-level check  
- `telnet/nc` → port-level connectivity  

---

### 6. Most Common Command

```bash
ping <host>
```

---

### 7. Interview-Ready Summary

“To test connectivity to a remote host, I typically start with ping to check basic reachability and latency. If needed, I use traceroute to identify network path issues, curl or wget for application-level testing, and telnet or netcat to verify if specific ports are open and accessible.”

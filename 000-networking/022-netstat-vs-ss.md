### Question  
What is the use of `netstat` and `ss`, and how do they differ?

---

### Answer  

---

### 1. What Are They Used For?

Both `netstat` and `ss` are used to inspect:

- Network connections  
- Open ports  
- Sockets  
- Routing tables  

---

### 2. Tool Overview

| Tool          | Purpose                                                                               |
| ------------- | ------------------------------------------------------------------------------------- |
| **`netstat`** | Displays network connections, routing tables, interface stats (legacy tool)           |
| **`ss`**      | Shows socket statistics, faster and more detailed (modern replacement for `netstat`)  |

---

### 3. Key Differences

| Feature          | `netstat`                   | `ss`                                          |
| ---------------- | --------------------------- | --------------------------------------------- |
| **Package**      | `net-tools` (deprecated)    | `iproute2` (modern, maintained)               |
| **Speed**        | Slower (reads from `/proc`) | Faster (reads directly from kernel)           |
| **IPv6 Support** | Limited                     | Full support                                  |
| **Detail Level** | Basic                       | More detailed socket information              |
| **Default**      | Older systems               | Modern Linux distributions                    |
| **Filtering**    | Limited                     | Advanced filtering options                    |

---

### 4. Common Usage Examples

---

#### 4.1 View Listening TCP Ports

```bash
netstat -tln
ss -tln
```

---

#### 4.2 Show All Connections (TCP/UDP)

```bash
netstat -tun
ss -tun
```

---

#### 4.3 Show Connections with Process Info

```bash
netstat -tunp
ss -tunp
```

---

#### 4.4 Display Listening Ports Only

```bash
netstat -l
ss -l
```

---

### 5. Why `ss` is Preferred

- Faster execution  
- More accurate data  
- Better filtering  
- Actively maintained  

---

### 6. Key Takeaways

- `netstat` → legacy tool  
- `ss` → modern replacement  
- Use `ss` for:
  - Debugging  
  - Performance analysis  

---

### 7. Interview-Ready Summary

“netstat and ss are used to inspect network connections and sockets. netstat is an older tool from the net-tools package, while ss is the modern replacement from iproute2. ss is faster, provides more detailed information, and is preferred in modern Linux systems.”

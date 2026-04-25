### Question  
How can you monitor real-time network traffic on Linux?

---

### Answer  

There are multiple tools in Linux to monitor network traffic in real time, depending on the level of detail you need.

---

### 1. `iftop` – Interface Bandwidth Usage

```bash
sudo iftop
```

#### Features:

- Shows real-time bandwidth usage  
- Displays:
  - Source ↔ Destination traffic  
- Similar to `top` but for network  

---

#### Install:

```bash
sudo apt install iftop       # Debian/Ubuntu
sudo yum install iftop       # CentOS/RHEL
```

---

### 2. `nload` – Simple Graph View

```bash
sudo nload
```

#### Features:

- Real-time incoming/outgoing traffic  
- Graph-based display  
- Easy to understand  

---

#### Install:

```bash
sudo apt install nload
```

---

### 3. `ip -s link` – Interface Statistics

```bash
ip -s link
```

#### Features:

- Shows:
  - Packets  
  - Bytes  
  - Errors  
- Built-in tool (no installation required)  

---

### 4. `tcpdump` – Packet-Level Monitoring

```bash
sudo tcpdump -i eth0
```

---

#### Features:

- Captures live packets  
- Deep analysis  
- Useful for debugging  

---

#### Example:

```bash
sudo tcpdump -i eth0 port 80
```

- Shows HTTP traffic  

---

### 5. `bmon` – Bandwidth Monitor

```bash
sudo bmon
```

#### Features:

- Terminal-based graphs  
- Per-interface monitoring  

---

#### Install:

```bash
sudo apt install bmon
```

---

### 6. `netstat` / `ss` – Connection Monitoring

```bash
netstat -tunp
ss -tunp
```

---

#### Real-time with watch:

```bash
watch -n 1 ss -tunp
```

---

### 7. `vnstat` – Live + Historical

```bash
vnstat -l -i eth0
```

#### Features:

- Live monitoring  
- Historical tracking  

---

#### Install:

```bash
sudo apt install vnstat
```

---

### 8. Key Takeaways

- `iftop` → bandwidth per connection  
- `nload` → simple traffic graph  
- `tcpdump` → packet-level analysis  
- `ss` → active connections  
- `vnstat` → long-term tracking  

---

### 9. Interview-Ready Summary

“To monitor real-time network traffic in Linux, I use tools like iftop and nload for bandwidth usage, tcpdump for packet-level inspection, and ss for active connections. For long-term and live monitoring, vnstat is useful. The choice depends on whether I need high-level bandwidth stats or deep packet analysis.”

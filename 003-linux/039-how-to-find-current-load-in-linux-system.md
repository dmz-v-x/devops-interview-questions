### Question  
What is the command to find the current load in a Linux system?

---

### Answer  

To check the current system load in Linux, you can use the following commands:

---

### 1. Using `uptime` (Most Common)

```bash
uptime
```

#### What it shows:
- System uptime  
- Number of logged-in users  
- Load averages for:
  - Last 1 minute  
  - Last 5 minutes  
  - Last 15 minutes  

---

#### Example Output:

```
15:42:10 up 5 days,  3:21,  2 users,  load average: 0.45, 0.50, 0.55
```

---

### 2. Using `top`

```bash
top
```

#### Features:
- Interactive process monitoring  
- Real-time updates  

#### Load Info:
- Displayed at the top:
  - 1, 5, and 15-minute load averages  

---

### 3. Using `/proc/loadavg`

```bash
cat /proc/loadavg
```

#### Description:
- Reads load average directly from the Linux kernel  

---

### 4. Using `htop` (if installed)

```bash
htop
```

#### Features:
- User-friendly interface  
- Color-coded stats  
- Easier navigation than `top`  

---

### 5. Quickest Way

```bash
uptime
```

---

### 6. Key Takeaways

- Load average represents system demand over time  
- `uptime` → quickest and simplest  
- `top` / `htop` → detailed and interactive  
- `/proc/loadavg` → raw kernel data  

---

### 7. Interview-Ready Summary

“To check the current load in Linux, I use the uptime command, which shows load averages for 1, 5, and 15 minutes. For more detailed monitoring, I use top or htop, which provide real-time system and process-level insights.”

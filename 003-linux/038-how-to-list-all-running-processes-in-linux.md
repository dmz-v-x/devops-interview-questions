### Question  
How do you list all running processes in Linux?

---

### Answer  

To list all running processes in Linux, you can use several commands depending on the level of detail and interactivity you need:

---

### 1. Using `ps`

```bash
ps aux
```

#### Explanation:

- `a` → shows processes for all users  
- `u` → displays the user/owner of the process  
- `x` → includes processes not attached to a terminal  

---

#### Example Output Columns:

- `USER` → owner of the process  
- `PID` → process ID  
- `%CPU / %MEM` → CPU and memory usage  
- `COMMAND` → command that started the process  

---

### 2. Using `top`

```bash
top
```

#### Features:

- Interactive display  
- Processes sorted by CPU usage by default  
- Real-time updates  

#### Controls:
- Press `q` to quit  

---

### 3. Using `htop` (if installed)

```bash
htop
```

#### Features:

- More user-friendly than `top`  
- Supports:
  - Scrolling  
  - Searching  
  - Killing processes easily  

---

### 4. Using `ps -ef`

```bash
ps -ef
```

#### Details:

- Displays all processes in full-format listing  

#### Common Columns:

- `UID` → user ID  
- `PID` → process ID  
- `PPID` → parent process ID  
- `C` → CPU usage  
- `STIME` → start time  
- `TTY` → terminal  
- `TIME` → CPU time used  
- `CMD` → command  

---

### 5. Quick One-Liner

```bash
ps aux
```

---

### 6. Key Takeaways

- `ps aux` → most common, static snapshot  
- `top` / `htop` → real-time monitoring  
- `ps -ef` → detailed process hierarchy  

---

### 7. Interview-Ready Summary

“To list all running processes in Linux, I commonly use ps aux for a quick snapshot of all processes. For real-time monitoring, I use top or htop, which provide interactive views of CPU and memory usage. If I need detailed process hierarchy information, I use ps -ef.”

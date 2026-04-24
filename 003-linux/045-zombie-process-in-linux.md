### Question  
What are zombie processes in Linux?

---

### Answer  

---

### 1. Definition

- A **zombie process** is a process that has **finished execution** but still exists in the process table  
- Its **exit status has not been read by its parent process**  

Also called: **defunct process**

---

### 2. Why do zombie processes occur?

- When a child process terminates:
  - It sends exit status to parent  
- Parent must call:
```bash
wait()
```

- If parent **does not call `wait()`**, the process remains as a zombie  

Common cause:
- Buggy or poorly written parent process  

---

### 3. Identification

```bash
ps aux | grep Z
```

or

```bash
ps -el | grep Z
```

---

#### Example Output:

```
Z  1234  567  0  80   0 -     0 exit   ?    00:00:00 defunct
```

- `Z` → Zombie state  

---

### 4. Characteristics

- Process is **dead (not running)**  
- No memory or CPU usage  
- Still occupies:
  - Process ID (PID)  
  - Entry in process table  

---

### 5. Impact

- Minimal for small numbers  
- But:
  - Too many zombies → exhaust PID table  
  - Can prevent new processes from starting  

---

### 6. Cleanup / Resolution

---

#### Method 1: Fix Parent Process (Best)

- Ensure parent calls:
```c
wait()
```

---

#### Method 2: Kill Parent Process

```bash
kill -9 <PPID>
```

- Zombie is adopted by:
  - `init` (PID 1) or systemd  
- Then cleaned automatically  

---

#### Method 3: Restart Service

- Restart the application creating zombies  

---

### 7. Key Difference: Zombie vs Orphan

| Type     | Description                                      |
| -------- | ------------------------------------------------ |
| Zombie   | Child finished, parent didn’t read exit status   |
| Orphan   | Parent died, child still running                 |

---

### 8. Interview-Ready Summary

“A zombie process is a terminated process whose exit status has not been collected by its parent process. It remains in the process table with a ‘Z’ state. While it does not consume CPU or memory, it still occupies a PID. To resolve it, we either fix the parent process to call wait() or terminate the parent so the init/systemd process can clean it up.”

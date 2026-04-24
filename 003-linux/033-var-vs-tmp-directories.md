### Question  
What is the difference between `/var` and `/tmp` directories?

---

### Answer  

---

### 1. `/var` Directory

#### Purpose

- `/var` stands for **variable data**  
- It stores files that are expected to **grow or change frequently** while the system is running  

---

#### Common Contents

| Subdirectory | Purpose                                          |
| ------------ | ------------------------------------------------ |
| `/var/log`   | System and application log files                 |
| `/var/spool` | Mail queues, print queues, cron jobs             |
| `/var/tmp`   | Temporary files that need to survive reboots     |
| `/var/lib`   | Application state data (databases, package info) |

---

#### Characteristics

- Data is **persistent**; survives reboots  
- Can grow in size → **monitoring disk space is important**  

---

#### Use Case

- Storing logs from Nginx, Apache, or system services  

Example:
```
/var/log/syslog  
/var/log/nginx/access.log
```

---

### 2. `/tmp` Directory

#### Purpose

- `/tmp` is used for **temporary files** created by applications or users  

---

#### Characteristics

- Data is **not persistent**; usually lost after reboot  
- Usually **world-writable**  

Permissions:
```
drwxrwxrwt
```

---

#### Use Case

- Storing temporary session files  
- Intermediate processing files  

Example:
```
/tmp/session12345
```

---

### 3. Key Differences

| Feature               | `/var`                                       | `/tmp`                          |
| --------------------- | -------------------------------------------- | ------------------------------- |
| Full Form             | Variable                                     | Temporary                       |
| Purpose               | Persistent, changing system/application data | Temporary files for runtime     |
| Data Lifetime         | Survives reboots                             | Usually cleared on reboot       |
| Common Subdirectories | `/var/log`, `/var/spool`, `/var/lib`         | None (just temporary storage)   |
| Access                | Mostly root-owned                            | World-writable with sticky bit  |
| Example               | `/var/log/syslog`                            | `/tmp/tempfile.txt`             |

---

### 4. Real-World Example

#### Scenario: Running a web server

- Persistent logs:
```
/var/log/nginx/access.log
```

- Temporary cache:
```
/tmp/nginx-cache
```

- Cache files can be safely deleted after server restart  

---

### 5. Tricky Interview Questions

---

#### Q: What’s the difference between `/var/tmp` and `/tmp`?  
**A:**  
- `/tmp` → cleared on reboot  
- `/var/tmp` → persists across reboots  

---

#### Q: Can you store critical data in `/tmp`?  
**A:**  
- No, because it may be deleted on reboot  
- Use `/var` or `/home` instead  

---

#### Q: What is the sticky bit on `/tmp`?  
**A:**  
- Ensures only the file owner can delete their files  
- Even though `/tmp` is world-writable  

---

#### Q: Why is `/var` important for monitoring disk space?  
**A:**  
- Logs, caches, and spool files grow over time  
- Can fill disk and affect system stability  

---

### 6. Interview-Ready Summary

“`/var` stores persistent and frequently changing system data like logs and application state, while `/tmp` is used for temporary files that are usually deleted after reboot. `/var` must be monitored for disk usage, whereas `/tmp` is mainly for short-lived runtime data.”

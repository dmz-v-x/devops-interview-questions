### Question  
How do you find and list the log files older than 7 days in the /var/log folder?

---

### Answer  

---

### 1. Basic Command

```bash
find /var/log -type f -mtime +7
```

---

### 2. Command Breakdown

- `find` → Command to search files/directories  
- `/var/log` → Target directory containing log files  
- `-type f` → Search only files (exclude directories)  
- `-mtime +7` → Files modified **more than 7 days ago**  

- Key understanding:
  - `+7` → Older than 7 days  
  - `-7` → Modified within last 7 days  
  - `7` → Exactly 7 days  

---

### 3. View Detailed File Information

```bash
find /var/log -type f -mtime +7 -exec ls -lh {} \;
```

- Shows:
  - File size  
  - Permissions  
  - Timestamp  

---

### 4. Count Matching Files

```bash
find /var/log -type f -mtime +7 | wc -l
```

- Useful to estimate cleanup impact  

---

### 5. Delete Old Log Files (Cleanup)

```bash
sudo find /var/log -type f -mtime +7 -delete
```

- ⚠️ Use carefully:
  - Always verify before deleting  

---

### 6. Safer Deletion (Preview First)

```bash
find /var/log -type f -mtime +7 -print
```

Then delete:

```bash
sudo find /var/log -type f -mtime +7 -exec rm -i {} \;
```

- `-i` → Prompts before deletion  

---

### 7. Key Takeaways

- `find` is powerful for file management  
- `-mtime` helps filter based on file age  
- Always:
  - Verify before deleting  
  - Use safe deletion practices  

---

### 8. Interview-Ready Summary

“To find log files older than 7 days, I use the find command with -mtime +7, which filters files modified more than 7 days ago. I can list them, inspect details using ls, and optionally delete them using -delete or -exec rm, ensuring I verify the files before cleanup.”

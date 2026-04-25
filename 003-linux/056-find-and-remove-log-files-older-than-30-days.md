### Question  
How do you find and remove log files older than 30 days using -exec in a folder?

---

### Answer  

---

### 1. Basic Command

```bash
sudo find /path/to/folder -type f -name "*.log" -mtime +30 -exec rm -f {} \;
```

**Example:**

```bash
sudo find /var/log -type f -name "*.log" -mtime +30 -exec rm -f {} \;
```

---

### 2. Command Breakdown

- `sudo` → Required for protected directories (e.g., `/var/log`)  
- `find` → Command to search files  
- `/path/to/folder` → Target directory  
- `-type f` → Only files (exclude directories)  
- `-name "*.log"` → Filter `.log` files  
- `-mtime +30` → Files older than 30 days  

- `-exec rm -f {} \;`:
  - `-exec` → Execute a command on each matched file  
  - `rm -f` → Force delete file  
  - `{}` → Placeholder for file path  
  - `\;` → End of command  

---

### 3. Safer Approach (Preview Before Deletion)

```bash
find /path/to/folder -type f -name "*.log" -mtime +30
```

- Always verify files before deleting  

---

### 4. Interactive Deletion (Safer)

```bash
sudo find /path/to/folder -type f -name "*.log" -mtime +30 -exec rm -i {} \;
```

- `-i` → Prompts before deleting each file  

---

### 5. More Efficient Alternative

```bash
sudo find /path/to/folder -type f -name "*.log" -mtime +30 -exec rm -f {} +
```

- `+` → Executes `rm` on multiple files at once  
- More efficient than `\;` (runs once per file)  

---

### 6. Key Takeaways

- `-exec` allows running commands on matched files  
- `-mtime +30` ensures only old files are targeted  
- Always:
  - Preview results before deletion  
  - Use safer options (`-i`) when needed  

---

### 7. Interview-Ready Summary

“To remove log files older than 30 days, I use the find command with -mtime +30 and -exec rm. For example, sudo find /var/log -type f -name '*.log' -mtime +30 -exec rm -f {} \;. This finds all .log files older than 30 days and deletes them. I usually preview the files first or use interactive mode to avoid accidental deletion.”

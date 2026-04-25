### Question  
How do you find and delete files larger than 100MB from a given directory?

---

### Answer  

---

### 1. Basic Command

```bash
find /path/to/directory -type f -size +100M -exec rm -f {} \;
```

---

### 2. Command Breakdown

- `find` → Searches files and directories  
- `/path/to/directory` → Target directory (e.g., `/var/log`, `/tmp`)  
- `-type f` → Only files (excludes directories)  
- `-size +100M` → Files larger than 100 MB  

- `-exec rm -f {} \;`:
  - `-exec` → Executes a command on each matched file  
  - `rm -f` → Force deletes file  
  - `{}` → Placeholder for file path  
  - `\;` → End of command  

---

### 3. Preview Before Deletion (Dry Run)

```bash
find /path/to/directory -type f -size +100M -exec ls -lh {} \;
```

- Displays:
  - File size  
  - File path  

- Helps verify before deleting  

---

### 4. Safer Deletion (Interactive)

```bash
find /path/to/directory -type f -size +100M -exec rm -i {} \;
```

- `-i` → Prompts before deleting each file  

---

### 5. More Efficient Alternative

```bash
find /path/to/directory -type f -size +100M -exec rm -f {} +
```

- `+` → Deletes multiple files in one command  
- Faster than `\;` (runs once per file)  

---

### 6. Key Takeaways

- `-size +100M` targets large files  
- Always:
  - Preview results before deletion  
  - Use interactive mode when needed  

---

### 7. Interview-Ready Summary

“To find and delete files larger than 100MB, I use the find command with -size +100M and -exec rm. For example, find /path -type f -size +100M -exec rm -f {} \;. I usually perform a dry run first using ls to verify the files before deleting them to avoid accidental data loss.”

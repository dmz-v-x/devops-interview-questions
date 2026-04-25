### Question  
How do you remove the first and last line of a file using sed?

---

### Answer  

---

### 1. Command

```bash
sed '1d; $d' filename.txt
```

---

### 2. Command Breakdown

- `sed` → Stream editor used to process text line-by-line  

- `'1d'`  
  - `1` → First line  
  - `d` → Delete  
  - Deletes the **first line**  

- `'$d'`  
  - `$` → Last line of file  
  - `d` → Delete  
  - Deletes the **last line**  

- Combined:
  - Deletes both **first and last lines**  

---

### 3. Example

**Input (file.txt):**
```
Line 1
Line 2
Line 3
Line 4
Line 5
```

**Command:**

```bash
sed '1d; $d' file.txt
```

**Output:**
```
Line 2
Line 3
Line 4
```

---

### 4. Save Output to New File

```bash
sed '1d; $d' file.txt > trimmed.txt
```

- Writes result to `trimmed.txt`  
- Original file remains unchanged  

---

### 5. Edit File In-Place (Optional)

```bash
sed -i '1d; $d' file.txt
```

- Modifies the file directly  
- Use with caution  

---

### 6. Key Takeaways

- `1d` → Removes first line  
- `$d` → Removes last line  
- `sed` is efficient for line-based text processing  

---

### 7. Interview-Ready Summary

“To remove the first and last line of a file, I use sed with the command sed '1d; $d' filename.txt. Here, 1d deletes the first line and $d deletes the last line. I can also redirect the output to a new file or use -i for in-place editing if needed.”

### Question  
How do you get the list of users who logged into the system today?

---

### Answer  

---

### 1. Command

```bash
last | grep "$(date '+%a %b %e')" | awk '{print $1}' | sort | uniq
```

---

### 2. Command Breakdown

- `last`  
  - Displays login history from `/var/log/wtmp`  

- `date '+%a %b %e'`  
  - Formats today’s date to match `last` output  
  - Example:
    - `Thu Jun 13`  

  - Format specifiers:
    - `%a` → Weekday (short)  
    - `%b` → Month (short)  
    - `%e` → Day (space-padded)  

- `grep "$(date ...)"`  
  - Filters entries for **today’s date**  

- `awk '{print $1}'`  
  - Extracts usernames (first column)  

- `sort | uniq`  
  - Removes duplicates  
  - Outputs unique users  

---

### 3. Example Output

```
ubuntu
admin
deploy
```

- These are users who logged in **today**  

---

### 4. Verify Log Availability

```bash
ls -lh /var/log/wtmp
```

- If file is missing or rotated:
  - `last` may return no results  

---

### 5. Alternative Using Journal Logs

```bash
journalctl --since today | grep 'session opened'
```

- Useful for:
  - Systems using `systemd`  
  - When `wtmp` logs are unavailable  

---

### 6. Key Takeaways

- `last` reads login history from `wtmp`  
- Filtering by date helps isolate today's logins  
- Always verify log availability if output is empty  

---

### 7. Interview-Ready Summary

“To list users who logged in today, I use the last command filtered with today’s date format and extract usernames using awk. For example, last | grep "$(date '+%a %b %e')" | awk '{print $1}' | sort | uniq. If logs are unavailable, I can also check journal logs using journalctl.”

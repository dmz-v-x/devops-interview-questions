### Question  
How do you change the default shell for all users on a remote Linux machine?

---

### Answer  

---

### 1. Change Default Shell for New Users

Edit the file:

```bash
sudo nano /etc/default/useradd
```

Update:

```bash
SHELL=/bin/bash
```

---

#### Explanation:

- This sets the **default shell for all new users** created after this change  
- Existing users are **not affected**  

---

### 2. Verify Default Shell Setting

```bash
useradd -D
```

Look for:

```
SHELL=/bin/bash
```

---

### 3. Change Shell for Existing Users

To update shell for existing users:

```bash
sudo chsh -s /bin/bash username
```

---

#### Example:

```bash
sudo chsh -s /bin/bash test
```

---

### 4. Change Shell for All Existing Users (Bulk)

```bash
for user in $(cut -f1 -d: /etc/passwd); do
  sudo chsh -s /bin/bash $user
done
```

---

### 5. Verify User Shell

```bash
grep username /etc/passwd
```

Output format:

```
username:x:1001:1001::/home/username:/bin/bash
```

---

### 6. Common Shells

- `/bin/bash` → most common  
- `/bin/sh` → minimal shell  
- `/bin/zsh` → advanced shell  
- `/sbin/nologin` → disable login  

---

### 7. Key Takeaways

- `/etc/default/useradd` → affects **new users only**  
- `chsh` → used for existing users  
- Shell defined in `/etc/passwd`  

---

### 8. Interview-Ready Summary

“To change the default shell for all new users, I update the SHELL variable in /etc/default/useradd. For existing users, I use the chsh command to modify their shell individually or in bulk. The shell configuration is stored in /etc/passwd.”

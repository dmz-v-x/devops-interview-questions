### Question  
Root user has created a file `secret.txt` which must not be accessed by anyone except root and another user `test`. How can this be achieved?

---

### Answer  

To restrict access so that only **root** and a specific user (`test`) can access the file, we can use **Linux ownership and permissions**.

---

### 1. Create a Group and Add User

```bash
sudo groupadd test_group
sudo usermod -aG test_group test
```

- Create a group (`test_group`)  
- Add user `test` to this group  

---

### 2. Change File Ownership

```bash
sudo chown root:test_group secret.txt
```

- Owner → `root`  
- Group → `test_group`  

---

### 3. Set Permissions

```bash
sudo chmod 640 secret.txt
```

#### Meaning:
- `6` → Owner (root) → read + write  
- `4` → Group (test_group) → read only  
- `0` → Others → no access  

---

### 4. Requirements

- User `test` must belong to `test_group`:

```bash
sudo usermod -aG test_group test
```

- User may need to re-login for group changes to take effect  

---

### 5. Result

| User Type | Access       |
| --------- | ------------ |
| root      | Read + Write |
| test      | Read         |
| others    | No access    |

---

### 6. Optional (Stronger Control using ACL)

If more granular control is needed:

```bash
setfacl -m u:test:r secret.txt
setfacl -m o::--- secret.txt
```

---

### 7. Key Takeaways

- Use **group-based permissions** for controlled access  
- `chmod 640` ensures strict access control  
- ACLs can be used for advanced permission handling  

---

### 8. Interview-Ready Summary

“To restrict a file so only root and a specific user can access it, I assign the file to a group, add that user to the group, and set permissions to 640. This ensures root has full access, the user has limited access, and all others are denied.”

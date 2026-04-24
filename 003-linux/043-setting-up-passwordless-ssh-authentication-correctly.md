### Question  
You have set up passwordless SSH authentication between two Linux machines, but it still prompts for a password. What could be wrong and what should you check?

---

### Answer  

If SSH key-based authentication is not working, the issue is usually related to permissions, configuration, or key setup. Here are the key things to verify:

---

### 1. Check Permissions

SSH is very strict about permissions.

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

- `.ssh` directory → only accessible by the user  
- `authorized_keys` → must not be publicly readable  

---

### 2. Check Ownership

```bash
chown user:user -R ~/.ssh
```

- Ensure the correct user owns:
  - `.ssh` directory  
  - `authorized_keys` file  

---

### 3. Verify SELinux (if enabled)

```bash
restorecon -Rv ~/.ssh
```

- Fixes SELinux context issues that may block SSH access  

---

### 4. Check SSH Server Configuration

Edit:
```bash
/etc/ssh/sshd_config
```

Ensure:

```
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

After changes:

```bash
sudo systemctl restart sshd
```

---

### 5. Verify Public Key Format

- Public key must be **single line**  

Example:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ... user@host
```

- No line breaks or extra spaces  

---

### 6. Ensure Correct Key is Used

```bash
ssh -i ~/.ssh/id_rsa user@host
```

- Confirm the correct private key is used  

---

### 7. Check SSH Debug Output

```bash
ssh -v user@host
```

- Look for:
  - `Offering public key`  
  - `Authentication succeeded`  
  - Or errors like `Permission denied`  

---

### 8. Verify authorized_keys Location

- Ensure file exists at:

```
~/.ssh/authorized_keys
```

- Not in wrong path or filename  

---

### 9. Check Home Directory Permissions

```bash
chmod 755 ~
```

- Home directory should not be writable by others  

---

### 10. Restart SSH Service

```bash
sudo systemctl restart sshd
```

---

### 11. Common Mistakes

- Wrong permissions on `.ssh` or files  
- Incorrect key copied  
- Wrong user or host  
- SSH config disabled key authentication  
- SELinux blocking access  

---

### 12. Interview-Ready Summary

“If passwordless SSH is not working, I check permissions of the .ssh directory and authorized_keys file, verify ownership, ensure correct SSH server configuration, validate the public key format, and use ssh -v for debugging. Most issues are due to incorrect permissions or misconfigured sshd settings.”

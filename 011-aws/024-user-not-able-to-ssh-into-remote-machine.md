### Question  
What could be the reason if a user is not able to SSH into a remote machine?

---

### 1. Overview

SSH connection failures can occur due to:
- Network issues  
- Service issues  
- Firewall restrictions  
- Authentication problems  
- Configuration mismatches  

---

### 2. Possible Causes and Troubleshooting

---

### 2.1 Network Issues

- Check connectivity:

```bash
ping remote_host
```

#### If fails:
- DNS issue  
- Host unreachable  
- Network routing problem  

---

### 2.2 SSH Service Down

- Verify SSH service status:

```bash
systemctl status sshd
```

#### If inactive:
- Start service:

```bash
sudo systemctl start sshd
```

---

### 2.3 Firewall Blocking SSH

- Check firewall rules:

```bash
sudo ufw status
```

#### Ensure:
- Port 22 is allowed  

```bash
sudo ufw allow 22
```

---

### 2.4 Authentication Errors

#### Common issues:

- Incorrect permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

- Missing public key:
  - Ensure correct key exists in:
    ```bash
    ~/.ssh/authorized_keys
    ```

---

### 2.5 SSH Port Change

- Check SSH configuration:

```bash
/etc/ssh/sshd_config
```

#### Look for:
```bash
Port <custom_port>
```

- Connect using custom port:

```bash
ssh -p <port> user@host
```

---

### 3. Additional Checks

- Wrong username  
- Incorrect private key  
- Security group / NACL blocking (in cloud environments)  
- SELinux restrictions  
- Disk full causing SSH failure  

---

### 4. Key Takeaways

- Always check network connectivity first  
- Ensure SSH service is running  
- Verify firewall and port settings  
- Validate authentication and permissions  

---

### 5. Interview-Ready Summary

“If a user cannot SSH into a remote machine, I first check network connectivity using ping. Then I verify if the SSH service is running using systemctl status sshd. I check firewall rules to ensure port 22 is open. Next, I validate authentication by checking key permissions and ensuring the public key is present in authorized_keys. Finally, I confirm whether SSH is running on a non-default port by checking sshd_config.”

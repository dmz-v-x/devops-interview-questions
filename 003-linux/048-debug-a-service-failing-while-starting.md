### Question  
How will you debug a service if it is failing while starting?

---

### Answer  

When a service fails to start, I follow a **systematic debugging approach** to identify the root cause.

---

### 1. Check Service Status

```bash
systemctl status <service-name>
```

- Shows:
  - Error messages  
  - Exit codes  
  - Recent logs  

---

### 2. Check Detailed Logs

```bash
journalctl -u <service-name> -xe
```

- Provides detailed error output  
- Helps identify:
  - Missing dependencies  
  - Permission issues  
  - Runtime errors  

---

### 3. Verify Configuration Files

- Check config syntax:

```bash
nginx -t        # example
apachectl configtest
```

- Look for:
  - Typos  
  - Wrong paths  
  - Invalid parameters  

---

### 4. Check Port Conflicts

```bash
netstat -tulnp | grep <port>
```

or

```bash
ss -tulnp | grep <port>
```

- If port already in use → service won’t start  

---

### 5. Check Permissions

- Ensure service has access to:
  - Config files  
  - Log directories  
  - Data directories  

```bash
ls -l /path
```

---

### 6. Check Dependencies

- Some services depend on others  

```bash
systemctl list-dependencies <service-name>
```

- Example:
  - Database service must be running before app  

---

### 7. Check Resource Limits

```bash
df -h
free -m
top
```

- Issues:
  - Disk full  
  - Low memory  
  - High CPU  

---

### 8. Check Environment Variables

- Missing env variables can break startup  

```bash
printenv
```

---

### 9. Run Service Manually

```bash
<service-binary> --debug
```

- Helps see direct error output  

---

### 10. Check SELinux / Firewall

```bash
getenforce
```

- If enforcing, may block service  

---

### 11. Restart and Retry

```bash
systemctl restart <service-name>
```

---

### 12. Check Core Dumps (if crash)

```bash
coredumpctl
```

---

### 13. Key Debug Flow

1. `systemctl status`  
2. `journalctl -xe`  
3. Check config  
4. Check ports  
5. Check permissions  
6. Check dependencies  

---

### 14. Common Causes

- Misconfigured config files  
- Port already in use  
- Missing dependencies  
- Permission issues  
- Resource exhaustion  
- Invalid environment variables  

---

### 15. Interview-Ready Summary

“If a service fails to start, I first check systemctl status and logs using journalctl to identify errors. Then I verify configuration files, check for port conflicts, validate permissions, and ensure dependencies are running. If needed, I run the service manually in debug mode to pinpoint the issue. This step-by-step approach helps isolate the root cause efficiently.”

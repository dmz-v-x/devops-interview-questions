### Question  
Your application runs fine locally, but when containerized and run with Docker, it crashes with a "Permission Denied" error. What could be the issue and how would you fix it?

---

### Answer  

---

### 1. Understanding the Problem

- Application works locally  
- Fails inside Docker with:
  - **Permission Denied**  

- Root cause:
  - File permissions or user access mismatch inside container  

---

### 2. Common Causes

- Missing execute permission on scripts  
- Running container as non-root user  
- Incorrect file ownership  
- Volume mount permission issues  

---

### 3. Issue 1: Missing Execute Permission

- Example:

```dockerfile
COPY start.sh /app/start.sh
CMD ["/app/start.sh"]
```

- Problem:
  - Script is not executable  

---

### Fix

```dockerfile
RUN chmod +x /app/start.sh
```

---

### 4. Issue 2: Non-Root User Restrictions

- Example:

```dockerfile
USER appuser
```

- Problem:
  - `appuser` may not have access to files  

---

### Fix

```dockerfile
RUN chown -R appuser:appuser /app
```

- Ensures:
  - Proper ownership and access  

---

### 5. Issue 3: Volume Mount Permission Issues

- Example:

```bash
docker run -v $(pwd)/data:/data myapp
```

- Problem:
  - Host files may not be readable by container user  

---

### Fix

```bash
chmod -R 755 data/
```

- Or:
  - Adjust ownership  

---

### 6. Debugging Steps

- Check permissions inside container:

```bash
docker exec -it <container_id> ls -l /app
```

- Run interactive shell:

```bash
docker run -it myapp /bin/sh
```

- Inspect:
  - File permissions  
  - Ownership  
  - User context  

---

### 7. Key Takeaways

- Containers may fail due to:
  - Permission mismatch  
  - User restrictions  

- Always verify:
  - `chmod` for executables  
  - `chown` for ownership  
  - Volume permissions  

---

### 8. Interview-Ready Summary

“This issue is usually caused by permission mismatches inside the container. I would check if scripts have execute permissions and ensure proper ownership when using non-root users. I’d also verify volume mount permissions, as host files may not be accessible to the container user. Debugging with ls -l and running the container interactively helps identify and fix the issue.”

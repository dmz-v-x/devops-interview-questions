### Question  
Your application is running inside a Docker container, but it's showing abnormal behavior. How would you debug it without stopping or restarting the container?

---

### Answer  

---

### 1. Approach Overview

- Goal:
  - Debug **live container** without downtime  

- Strategy:
  - Inspect:
    - Logs  
    - Processes  
    - Environment  
    - Network  
    - Filesystem  

---

### 2. Use docker exec (Primary Method)

```bash
docker exec -it <container_id> /bin/sh
```

OR:

```bash
docker exec -it <container_id> /bin/bash
```

- Allows:
  - Interactive shell inside container  

- Use cases:

```bash
cat /var/log/app.log
env
ls -l /app
```

---

### 3. Check Logs

```bash
docker logs -f <container_id>
```

- Shows:
  - STDOUT / STDERR  

- Useful for:
  - Runtime errors  
  - Crash messages  

---

### 4. Inspect Container Metadata

```bash
docker inspect <container_id>
```

- Check:
  - Environment variables  
  - Mounts  
  - Network config  

- Example:

```bash
docker inspect -f '{{.Config.Env}}' <container_id>
```

---

### 5. Check Running Processes

```bash
docker top <container_id>
```

- Helps:
  - Verify if app is running  
  - Detect stuck/zombie processes  

---

### 6. Debug Network Inside Container

```bash
docker exec -it <container_id> netstat -tulnp
```

```bash
docker exec -it <container_id> curl http://localhost:<port>
```

- Helps:
  - Verify port binding  
  - Check service availability  

---

### 7. Use docker attach (With Caution)

```bash
docker attach <container_id>
```

- Connects to:
  - Main process output  

- Warning:
  - `Ctrl+C` may stop container  
  - Use:
    - `Ctrl + P + Q` to detach safely  

---

### 8. Additional Debugging Checks

- File system:

```bash
docker exec -it <container_id> ls -l /app
```

- Permissions:

```bash
docker exec -it <container_id> id
```

- Resource usage:

```bash
docker stats <container_id>
```

---

### 9. Key Takeaways

- Use `docker exec` for safe debugging  
- Always check:
  - Logs  
  - Processes  
  - Network  
  - Environment  

- Avoid restarting:
  - Preserve runtime state  

---

### 10. Interview-Ready Summary

“To debug a running container without stopping it, I use docker exec to get an interactive shell and inspect logs, environment variables, files, and processes. I also use docker logs for runtime output, docker inspect for configuration details, and docker top to check running processes. For network issues, I test connectivity inside the container. This approach allows me to diagnose issues without impacting availability.”

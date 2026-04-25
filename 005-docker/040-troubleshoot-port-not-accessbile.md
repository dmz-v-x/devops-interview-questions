### Question  
Port is not accessible on localhost even after using -p flag to publish it. How do you troubleshoot?

---

### Answer  

---

### 1. Understand the Problem

- You are using:

```bash
docker run -p 8080:80 <image>
```

- But:
  - `localhost:8080` is not accessible  

- Possible issue areas:
  - Port mapping  
  - Application binding  
  - Firewall  
  - Container/app failure  

---

### 2. Verify Port Mapping

```bash
docker ps
```

- Check:
  - PORTS column shows:
    - `0.0.0.0:8080->80/tcp`  

- If not:
  - Re-run container with correct mapping  

---

### 3. Check if Host Port is Free

```bash
lsof -i :8080
```

```bash
netstat -tulnp | grep 8080
```

- If port is already in use:
  - Choose a different port  

---

### 4. Check Container Logs

```bash
docker logs <container_id>
```

- Look for:
  - App crashes  
  - Binding errors  
  - Startup failures  

---

### 5. Check Application Inside Container

- Enter container:

```bash
docker exec -it <container_id> /bin/bash
```

- Check listening ports:

```bash
netstat -tulnp
```

- Verify:
  - App is running  
  - Listening on expected port  

---

### 6. Critical Check: Binding Address

- Common issue:
  - App listens on `127.0.0.1` (localhost inside container)

- Example problem:

```python
app.run(host='127.0.0.1', port=5000)
```

- Result:
  - Container port is NOT accessible externally  

---

### 7. Fix: Bind to All Interfaces

```python
app.run(host='0.0.0.0', port=5000)
```

- Why:
  - `0.0.0.0` allows connections from:
    - Docker network  
    - Host machine  

---

### 8. Check Firewall Settings

```bash
sudo ufw status
```

- Ensure:
  - Port 8080 is allowed  

- Also check:

```bash
sudo iptables -L
```

---

### 9. Verify Network Mode

- Default:
  - Bridge network works fine  

- If using custom network:
  - Ensure proper configuration  

---

### 10. Key Takeaways

- `-p` only forwards traffic  
- App must:
  - Be running  
  - Listen on correct port  
  - Bind to `0.0.0.0`  

- Most common issue:
  - App bound to `127.0.0.1`  

---

### 11. Interview-Ready Summary

“If a port is not accessible even after using -p, I first verify the port mapping using docker ps and ensure the host port is free. Then I check container logs and confirm the application is running inside the container. A common issue is the app binding to 127.0.0.1 instead of 0.0.0.0, which prevents external access. I also verify firewall rules and ensure the correct network configuration. Fixing the binding to 0.0.0.0 usually resolves the issue.”

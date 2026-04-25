### Question  
Docker container exits immediately, how will you troubleshoot?

---

### Answer  

---

### 1. Understanding the Problem

- Docker containers follow:
  - **Single-process model**  

- Key behavior:
  - When the main process (CMD/ENTRYPOINT) finishes → container exits  

- Common reason:
  - Process is:
    - Short-lived (e.g., `echo "hello"`)  
    - Crashing due to error  
    - Misconfigured  

---

### 2. Common Causes

- CMD/ENTRYPOINT runs a short process  
- Application crashes on startup  
- Missing dependencies  
- Incorrect file paths or configs  
- Port binding issues  

---

### 3. Step-by-Step Troubleshooting

---

### Step 1: Check Container Logs

```bash
docker logs <container_id_or_name>
```

- Look for:
  - Errors  
  - Stack traces  
  - Missing files or dependencies  

---

### Step 2: Check Exit Code

```bash
docker inspect <container_id> --format='{{.State.ExitCode}}'
```

- `0` → Normal exit (likely short-lived process)  
- Non-zero → Error occurred  

---

### Step 3: Inspect Dockerfile (CMD / ENTRYPOINT)

- Example:

```dockerfile
CMD ["python", "app.py"]
```

- If `app.py`:
  - Finishes quickly → container exits  
  - Crashes → container exits  

- Ensure:
  - Long-running process (e.g., server)  

---

### Step 4: Run Container in Interactive Mode

```bash
docker run -it <image> /bin/bash
```

- Helps:
  - Debug environment  
  - Check files, dependencies, configs  

---

### Step 5: Check Running Process

Inside container:

```bash
ps aux
```

- Verify:
  - Expected process is running  

---

### Step 6: Validate Application Behavior

- Check:
  - Does the app exit immediately?  
  - Is it a background process?  

- Example issue:
  - Running script instead of server  

---

### Step 7: Use Detached Mode with Logs

```bash
docker run -d <image>
docker logs -f <container_id>
```

- Helps observe runtime behavior  

---

### 8. Fix Strategies

- Use proper long-running command:

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

- Avoid:
  - Short-lived commands like `echo`  

- Ensure:
  - Correct dependencies  
  - Valid configs  
  - Correct working directory  

---

### 9. Key Takeaways

- Container exits when:
  - Main process exits  

- Always check:
  - Logs  
  - Exit code  
  - CMD/ENTRYPOINT  

- Most issues are:
  - Misconfiguration  
  - App crash  
  - Short-lived process  

---

### 10. Interview-Ready Summary

“A Docker container exits when its main process defined in CMD or ENTRYPOINT finishes. To troubleshoot, I first check logs using docker logs to identify errors. Then I inspect the exit code to see if it failed or exited normally. I review the Dockerfile to ensure a long-running process is configured. If needed, I run the container in interactive mode to debug inside. Most commonly, containers exit due to application crashes or short-lived commands.”

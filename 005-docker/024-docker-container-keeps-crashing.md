### Question  
You encountered a problem where a Docker container keeps crashing without any clear error message. How would you troubleshoot and diagnose this issue?

---

### Answer  

### 1. Check Container Logs (First Step)  

    docker logs <container_id>
    docker logs -f <container_id>

- Shows stdout/stderr  
- Look for:
  - Exceptions  
  - Missing dependencies  
  - Config errors  

---

### 2. Check Container Status & Exit Code  

    docker ps -a

---

#### Get Exit Code  

    docker inspect <container_id> --format='{{.State.ExitCode}}'

---

#### Common Exit Codes  

| Code | Meaning |
|---|---|
| 0 | Normal exit |
| 1 | Application error |
| 137 | Killed (OOM) |
| 143 | SIGTERM (graceful stop) |

---

### 3. Inspect Detailed Container State  

    docker inspect <container_id>

Look for:

- `State`  
- `OOMKilled`  
- `Error`  
- `FinishedAt`  

---

### 4. Run Container Interactively  

Sometimes container exits too quickly.

---

#### Debug Mode  

    docker run -it --entrypoint /bin/bash <image>

---

Now you can:

- Check files  
- Verify configs  
- Run app manually  

---

### 5. Verify CMD / ENTRYPOINT  

Misconfigured command = instant exit

---

    docker inspect <container_id> | grep -i '"Cmd"'

---

Check:

- Correct executable  
- Correct arguments  

---

### 6. Check Resource Issues  

---

#### Memory / CPU Limits  

    docker inspect <container_id> | grep -i mem

---

#### Host Resources  

    docker info
    df -h

---

Look for:

- Low memory  
- Disk full  
- OOMKilled = true  

---

### 7. Override Entrypoint for Debugging  

    docker run -it --entrypoint sh <image>

---

- Keeps container alive  
- Run app manually step-by-step  

---

### 8. Check Dependency Failures  

If app depends on other services:

---

#### Example  

    docker exec -it <container_id> curl http://db:5432

---

Check:

- DB connectivity  
- API availability  
- DNS resolution  

---

### 9. Check Networking  

    docker network inspect <network>

---

- Ensure containers are on same network  
- Verify service names  

---

### 10. Check Image Issues  

- Incorrect build  
- Missing files  
- Wrong base image  

---

Rebuild:

    docker build --no-cache -t myapp .

---

### 11. Use Debugging Tools  

---

#### Monitor Resources  

    docker stats

---

#### Check Events  

    docker events

---

### 12. Key Troubleshooting Flow  

1. Logs  
2. Exit code  
3. Inspect container  
4. Run interactively  
5. Check resources  
6. Verify dependencies  

---

### 13. Tricky Interview Questions  

---

Why does container exit immediately?  

- Main process crashes or finishes  

---

What does Exit Code 137 mean?  

- Out of memory (OOM kill)  

---

How to debug fast-exiting container?  

- Override ENTRYPOINT  

---

What if logs are empty?  

- Check entrypoint / command  

---

### Interview Summary  

“I would start by checking container logs and exit codes to identify the failure reason. Then I’d inspect the container state, verify the CMD/ENTRYPOINT, and run the container interactively for deeper debugging. I’d also check resource limits, host capacity, and service dependencies. This step-by-step approach helps isolate and resolve container crashes effectively.”

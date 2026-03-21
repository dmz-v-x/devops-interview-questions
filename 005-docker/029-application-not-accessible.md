### Question  
Your Docker container is running but the application is not accessible. How would you troubleshoot and fix it? Also, why is cleanup needed in CI/CD pipelines?

---

### Answer  

## Part 1: Troubleshooting Container Not Accessible  

---

### 1. Check Container Logs  

    docker logs <container-id>

---

- Look for:
  - Application errors  
  - Missing configs  
  - Dependency failures  

---

### 2. Verify Application is Listening on Correct Port  

Inside container:

    docker exec -it <container-id> netstat -tuln

---

Check:

- App is running  
- Port is open  

---

⚠️ Important  

- App must bind to:

        0.0.0.0  

NOT:

        127.0.0.1  

---

### 3. Check Port Mapping  

When running container:

    docker run -p 8080:8080 myapp

---

Verify:

    docker ps

---

Example:

    0.0.0.0:8080->8080/tcp

---

If missing → app won’t be accessible  

---

### 4. Check Firewall / Security Rules  

---

- Local firewall (iptables, ufw)  
- Cloud security groups  

---

Ensure:

- Port (80 / 8080 / etc.) is open  

---

### 5. Check Docker Network  

---

    docker network inspect bridge

---

- Ensure container is reachable  
- Try host networking:

    docker run --network host myapp

---

### 6. Check Container Status  

    docker ps -a

---

Look for:

- Restarting  
- Exited  

---

If restarting → check logs  

---

### 7. Verify Environment Variables  

    docker exec -it <container-id> printenv

---

Check:

- DB_HOST  
- API keys  
- Config values  

---

### 8. Test Inside Container  

    docker exec -it <container-id> curl http://localhost:8080

---

- If works → issue is external  
- If fails → issue is app  

---

### 9. Common Root Causes  

---

- App binding to localhost  
- Missing port mapping  
- Firewall blocking  
- App crash  
- Dependency not reachable  

---

### Interview Summary 

“I would start by checking logs and ensuring the app is running and listening on the correct port (0.0.0.0). Then I’d verify port mapping, network configuration, and firewall rules. I’d also test connectivity from inside the container to isolate whether the issue is internal or external.”

---

## Part 2: Why Cleanup is Needed in CI/CD  

---

### 1. Disk Space Management  

- Images, containers, volumes accumulate  
- Can fill disk → pipeline failure  

---

### 2. Improved Performance  

- Less clutter → faster Docker operations  

---

### 3. Faster Builds  

- Reduces lookup time  
- Avoids stale cache issues  

---

### 4. Avoid Resource Exhaustion  

- Prevents:
  - Disk full errors  
  - Memory issues  

---

### 5. Cleaner Environment  

- Easier debugging  
- No conflicts from old resources  

---

### 6. Cleanup Commands (CI/CD)  

    docker system df
    docker system prune -af
    docker volume prune -f

---

### Interview Summary 

“Cleanup is essential in CI/CD pipelines to prevent disk space exhaustion, improve performance, and ensure a clean environment. I typically use `docker system prune -af` as part of the pipeline to remove unused resources and keep builds efficient and reliable.”

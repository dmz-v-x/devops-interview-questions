### Question  
After successfully executing the Docker command `docker run ubuntu`, the Ubuntu container exits immediately. What could be the reason?

---

### Answer  

### 1. Root Cause  

The container exits because **no long-running foreground process is running inside it**.

In Docker:

- A container runs **only as long as its main process (PID 1) is running**  
- Once that process exits → the container stops automatically  

---

### 2. What Happens Internally  

When you run:

    docker run ubuntu

Docker:

1. Creates a container  
2. Runs the default command of the Ubuntu image:

        CMD ["bash"]

3. Since:
   - No terminal is attached  
   - No interaction is provided  

`bash` starts and immediately exits  

→ Container stops  

---

### 3. Key Concept  

**Docker container lifecycle = lifecycle of its main process**

- Process running → container alive  
- Process exits → container stops  

---

### 4. Why Ubuntu Behaves This Way  

- Ubuntu is a **base image**  
- It does NOT run any service by default  
- No daemon / server is started  
- So nothing keeps the container alive  

---

### 5. How to Fix It  

---

#### Run Interactive Shell  

    docker run -it ubuntu /bin/bash

- `-i` → interactive  
- `-t` → terminal  
- `/bin/bash` → keeps process running  

---

#### Run Long-Running Process  

    docker run ubuntu tail -f /dev/null

- This command never exits  
- Keeps container alive  

---

#### Run a Specific Process  

    docker run ubuntu sleep 1000

---

### 6. Check Container Status  

    docker ps -a

- Shows container state (Exited, Running, etc.)

---

#### View Logs  

    docker logs <container_id>

- Helps debug why container stopped  

---

### 7. Comparison with Other Images  

| Image | Behavior | Reason |
|---|---|---|
| ubuntu | Exits immediately | No running process |
| nginx | Keeps running | Runs web server |
| mysql | Keeps running | Runs DB server |

---

### 8. Tricky Interview Questions  

---

Why do containers stop automatically?  

- Because the main process exits  

---

What is PID 1 in Docker?  

- The main process that controls container lifecycle  

---

Is a container like a VM?  

- No → container = process, not full OS  

---

How to keep any container alive?  

- Run a long-running foreground process  

---

### Interview Summary  

The Ubuntu container exits immediately because it does not run any long-lived process by default. Docker containers are tied to their main process, and once that process exits, the container stops. To keep it running, you must start a foreground process like `bash`, `sleep`, or `tail -f /dev/null`.

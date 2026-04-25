### Question  
What are the most common Docker commands you use regularly while working with containers?

---

### Answer  

---

### 1. Overview

- Common Docker commands help with:
  - Building images  
  - Running containers  
  - Debugging  
  - Cleanup and maintenance  

---

### 2. Frequently Used Commands

---

#### 1. List Containers

```bash
docker ps
```

- Shows running containers  

```bash
docker ps -a
```

- Shows all containers (including stopped ones)  

---

#### 2. Build Image

```bash
docker build -t myapp:latest .
```

- Builds image from Dockerfile  
- `-t` → Tag name  

---

#### 3. Run Container

```bash
docker run -d -p 8080:80 myapp
```

- `-d` → Detached mode  
- `-p` → Port mapping  

---

#### 4. Execute Inside Container

```bash
docker exec -it myapp_container /bin/bash
```

- Used for:
  - Debugging  
  - Running commands inside container  

---

#### 5. View Logs

```bash
docker logs -f myapp_container
```

- `-f` → Follow logs in real-time  

---

#### 6. Stop / Start Containers

```bash
docker stop myapp_container
docker start myapp_container
```

---

#### 7. List Images

```bash
docker images
```

- Shows:
  - Image name  
  - Tag  
  - Size  

---

#### 8. Remove Containers / Images

```bash
docker rm myapp_container
docker rmi myapp:latest
```

---

#### 9. Cleanup Unused Resources

```bash
docker system prune -a
```

- Removes:
  - Unused containers  
  - Images  
  - Networks  

---

#### 10. Inspect Container

```bash
docker inspect myapp_container
```

- Shows:
  - Environment variables  
  - Network settings  
  - Mount paths  

---

### 3. Key Takeaways

- Core workflow:
  - Build → Run → Debug → Clean  

- Essential commands:
  - `docker build`, `docker run`, `docker ps`, `docker logs`, `docker exec`  

- Maintenance:
  - `docker system prune` prevents disk issues  

---

### 4. Interview-Ready Summary

“I regularly use commands like docker build to create images, docker run to start containers, docker ps to check running containers, docker logs and docker exec for debugging, and docker system prune for cleanup. These commands cover the full lifecycle of building, running, monitoring, and maintaining containers.”

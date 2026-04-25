### Question  
Your Docker host is running out of disk space. What are the steps you'd take to clean up unused data and prevent this from happening again?

---

### Answer  

---

### 1. Understand the Problem

- Docker stores data in:
  - `/var/lib/docker`  

- Over time, disk fills up due to:
  - Stopped containers  
  - Unused images  
  - Dangling volumes  
  - Build cache  

---

### 2. Check Disk Usage

```bash
docker system df
```

- Shows:
  - Space used by images, containers, volumes, cache  

---

### 3. Clean Up Unused Resources

```bash
docker system prune
```

- Removes:
  - Stopped containers  
  - Unused networks  
  - Dangling images  
  - Build cache  

---

### 4. Deep Cleanup (Aggressive)

```bash
docker system prune -a --volumes
```

- Removes:
  - All unused images (not just dangling)  
  - All unused volumes  

- Use carefully:
- May delete important data  

---

### 5. Remove Unused Volumes

```bash
docker volume ls -f dangling=true
```

```bash
docker volume rm $(docker volume ls -qf dangling=true)
```

OR:

```bash
docker volume prune
```

---

### 6. Remove Large/Unused Images

```bash
docker images --format "{{.Repository}}:{{.Tag}}\t{{.Size}}"
```

```bash
docker rmi <image_id>
```

- Helps remove:
  - Large unused images  

---

### 7. Investigate Disk Usage

```bash
sudo du -sh /var/lib/docker/*
```

- Identifies:
  - Which components consume most space  

---

### 8. Preventive Measures

- Automate cleanup (cron):

```bash
0 3 * * 0 docker system prune -a --volumes -f
```

- Use smaller base images:
  - `alpine`  
  - `distroless`  

- Optimize Dockerfile:

```dockerfile
RUN apt-get update && apt-get install -y package \
 && rm -rf /var/lib/apt/lists/*
```

- Reduce:
  - Intermediate layers  
  - Unnecessary files  

---

### 9. Key Takeaways

- Docker does not auto-clean unused resources  
- Regular pruning is essential  
- Monitor disk usage proactively  

---

### 10. Interview-Ready Summary

“I would start by checking disk usage using docker system df, then clean up unused containers, images, volumes, and cache using docker system prune. For deeper cleanup, I’d use docker system prune -a --volumes cautiously. I would also remove large unused images and inspect /var/lib/docker to identify heavy usage. To prevent recurrence, I’d automate cleanup using cron and optimize Dockerfiles to reduce image size.”

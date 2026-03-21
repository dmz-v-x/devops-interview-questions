### Question  
How do you clean up unused Docker resources efficiently (especially in CI/CD pipelines)?

---

### Answer  

### 1. Why Cleanup is Important  

In CI/CD pipelines:

- Frequent builds → many images  
- Test containers → stopped containers  
- Temporary volumes/networks  

→ Leads to **disk space exhaustion** and performance issues  

---

### 2. Remove Stopped Containers  

    docker container prune -f

---

#### Alternative (Manual)  

    docker ps -a -f status=exited -q | xargs docker rm

---

### 3. Remove Unused Images  

---

#### Remove Dangling Images  

    docker image prune -f

---

#### Remove All Unused Images  

    docker image prune -a -f

---

⚠️ Warning:

- `-a` removes ALL unused images (even tagged ones)

---

#### Check Before Deleting  

    docker images

---

### 4. Remove Unused Volumes  

    docker volume prune -f

---

#### Check Dangling Volumes  

    docker volume ls -f dangling=true

---

### 5. Remove Unused Networks  

    docker network prune -f

---

#### List Networks  

    docker network ls

---

### 6. One Command Cleanup (Best for CI/CD)  

---

#### Basic Cleanup  

    docker system prune -f

Removes:

- Stopped containers  
- Unused networks  
- Dangling images  
- Build cache  

---

#### Full Cleanup  

    docker system prune -a -f

---

Removes:

- All unused images  
- Containers  
- Networks  
- Volumes  

---

⚠️ Use carefully in production  

---

### 7. Best Practice for CI/CD  

---

#### Step 1: Check Usage  

    docker system df

---

#### Step 2: Cleanup  

    docker system prune -af

---

#### Step 3: Automate  

- Add cleanup step in pipeline  
- Use cron jobs for periodic cleanup  

---

### 8. Safe Cleanup Strategy  

| Resource | Command |
|---|---|
| Containers | `docker container prune` |
| Images | `docker image prune -a` |
| Volumes | `docker volume prune` |
| Networks | `docker network prune` |
| All | `docker system prune -a` |

---

### 9. Tricky Interview Questions  

---

Does `docker system prune` remove running containers?  

- ❌ No  

---

What is a dangling image?  

- `<none>:<none>` image  

---

What is the risk of `-a` flag?  

- Removes all unused images  

---

Do volumes get removed by default?  

- ❌ Only with explicit prune  

---

### Interview Summary  

“To clean up unused Docker resources, I use prune commands like `docker container prune`, `docker image prune`, and `docker system prune -a`. In CI/CD pipelines, I automate cleanup to prevent disk space issues, while ensuring running containers and required images are not affected.”

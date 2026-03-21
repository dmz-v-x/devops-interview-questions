### Question  
There are multiple stopped containers and unused networks taking up space. How would you clean up these resources efficiently? Also, how do you check and change Docker’s root directory?

---

### Answer  

### 1. Why Cleanup is Needed  

- Stopped containers  
- Unused networks  
- Dangling/unused images  
- Volumes  

→ All consume disk space even when not in use  

---

### 2. Check Current Disk Usage  

Before cleanup:

    docker system df

- Shows space used by:
  - Images  
  - Containers  
  - Volumes  

---

### 3. Remove Stopped Containers  

    docker container prune

- Removes all stopped containers  

---

### 4. Remove Unused Networks  

    docker network prune

- Deletes networks not used by any container  

---

### 5. Remove Dangling Images  

    docker image prune

- Removes `<none>:<none>` images  

---

### 6. Full Cleanup (Recommended)  

    docker system prune

Removes:

- Stopped containers  
- Unused networks  
- Dangling images  
- Build cache  

---

#### Remove All Unused Images Too  

    docker system prune -a

⚠️ Warning:

- Removes ALL unused images (even tagged ones)

---

### 7. Remove Unused Volumes  

    docker volume prune

- Frees persistent storage  

---

### 8. Best Practice  

---

- Always check first:

    docker system df  

---

- Automate cleanup (non-production):

    cron jobs  

---

- Be cautious with:

    -a flag  

---

### 9. Interview-Ready Summary  

“I would clean unused resources using Docker prune commands:

    docker container prune
    docker network prune
    docker system prune -a

Before cleanup, I’d check disk usage with `docker system df`. This ensures efficient cleanup without affecting running containers.”

---

## 10. Docker Root Directory  

---

### Default Location  

    /var/lib/docker

---

### Verify Current Path  

    docker info | grep "Docker Root Dir"

---

### 11. Change Docker Root Directory  

---

#### Step 1: Stop Docker  

    sudo systemctl stop docker

---

#### Step 2: Create New Directory  

    sudo mkdir -p /new/path/docker

---

#### Step 3: Update Config  

    sudo nano /etc/docker/daemon.json

Add:

    {
      "data-root": "/new/path/docker"
    }

---

#### Step 4: Move Existing Data (Optional)  

    sudo rsync -aP /var/lib/docker /new/path/docker

---

#### Step 5: Start Docker  

    sudo systemctl start docker

---

#### Step 6: Verify  

    docker info | grep "Docker Root Dir"

---

### 12. Key Concepts  

---

- `/var/lib/docker` → stores all Docker data  
- Can be moved for:
  - Disk space management  
  - Performance optimization  

---

### 13. Tricky Interview Questions  

---

Does `docker system prune` remove running containers?  

- ❌ No  

---

What does `docker system prune -a` remove?  

- All unused images + other unused resources  

---

What happens if Docker root dir is deleted?  

- ❌ All data lost  

---

### Interview Summary  

To clean up Docker resources, use prune commands like `docker container prune`, `docker network prune`, and `docker system prune -a`. Always verify usage with `docker system df`. Docker stores its data in `/var/lib/docker` by default, and this location can be changed using the `data-root` setting in `daemon.json`.

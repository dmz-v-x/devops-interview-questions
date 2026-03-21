### Question  
What does the `docker system df` command do?

---

### Answer  

### 1. Purpose  

`docker system df` is used to:

👉 **Check disk usage of Docker resources**

---

It shows how much space is used by:

- Images  
- Containers  
- Volumes  
- Build cache  

---

### 2. Basic Command  

    docker system df

---

### 3. Example Output  

    TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
    Images          10        3         5GB       3GB
    Containers      5         2         200MB     150MB
    Local Volumes   4         1         1.2GB     900MB
    Build Cache     0         0         0B        0B

---

### 4. Output Explanation  

| Column | Meaning |
|---|---|
| TOTAL | Total number of objects |
| ACTIVE | Currently used (running or referenced) |
| SIZE | Total disk space used |
| RECLAIMABLE | Space that can be freed |

---

### 5. Key Insight  

- **RECLAIMABLE ≠ automatically deleted**  
- You must manually clean it  

---

### 6. Clean Up Based on Output  

---

#### Remove unused resources  

    docker system prune

---

#### Remove everything unused  

    docker system prune -a

---

⚠️ Warning:

- `-a` removes all unused images  

---

### 7. Detailed View (Optional)  

    docker system df -v

---

- Shows per-image and per-container usage  

---

### 8. When to Use  

---

- Before cleanup  
- Disk space troubleshooting  
- CI/CD maintenance  

---

### 9. Tricky Interview Questions  

---

Does it delete anything?  

- ❌ No (read-only command)  

---

What is reclaimable space?  

- Space from unused resources  

---

Does it include running containers?  

- ✅ Yes (in ACTIVE column)  

---

### Interview Summary  

“The `docker system df` command helps analyze disk usage of Docker resources like images, containers, volumes, and build cache. It shows total, active, and reclaimable space, helping decide what can be cleaned using commands like `docker system prune`.”

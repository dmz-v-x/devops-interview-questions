### Question  
Your team needs to share data between multiple Docker containers. How would you accomplish this while maintaining isolation between the containers?

---

### Answer  

### 1. Use Docker Volumes (Best Practice)  

Docker volumes are the **recommended way** to share data between containers.

---

#### Step 1: Create Volume  

    docker volume create shared-data

---

#### Step 2: Attach Volume to Containers  

    docker run -d --name app1 -v shared-data:/usr/share/app/data myapp:latest
    docker run -d --name app2 -v shared-data:/usr/share/app/data myapp:latest

---

#### Result  

- Both containers access:

        /usr/share/app/data  

- Data is:
  - Shared  
  - Persistent  
  - Independent of container lifecycle  

---

#### Why This Maintains Isolation  

- Containers:
  - Have separate processes  
  - Have separate filesystems (except shared volume)  
- Only **specific directory is shared**  

---

### 2. Use Bind Mounts (Development Use Case)  

---

#### Example  

    docker run -d --name app1 -v /host/data:/app/data myapp
    docker run -d --name app2 -v /host/data:/app/data myapp

---

#### Pros  

- Easy file sharing  
- Useful for local development  

---

#### Cons  

- Depends on host path  
- Less portable  
- Security risk if misconfigured  

---

### 3. Data-Only Containers (Legacy)  

---

#### Example  

    docker create -v /data --name data-container busybox
    docker run --volumes-from data-container app1
    docker run --volumes-from data-container app2

---

⚠️ Not recommended anymore  
→ Replaced by named volumes  

---

### 4. Service-Based Sharing (Best for Microservices)  

Instead of sharing files directly:

- Use a **data service container** (DB, Redis, API)

---

#### Example  

- App containers communicate via network:

        docker network create app-net

---

- Use services:

  - Database  
  - Cache  
  - API layer  

---

#### Benefits  

- Strong isolation  
- Controlled access  
- Better scalability  

---

### 5. Key Concept  

**Isolation + Controlled Sharing**

- Share only what is needed (volume path)  
- Keep rest of container isolated  

---

### 6. Comparison  

| Method | Use Case | Isolation | Recommended |
|---|---|---|---|
| Named Volume | Production | High | ✅ Yes |
| Bind Mount | Development | Medium | ⚠️ Limited |
| Data Container | Legacy | Medium | ❌ No |
| Service/API | Microservices | Very High | ✅ Best |

---

### 7. Tricky Interview Questions  

---

Can containers share full filesystem?  

- ❌ Not recommended  

---

What happens if container is deleted?  

- Volume data persists  

---

Can multiple containers write to same volume?  

- ✅ Yes (handle concurrency carefully)  

---

Best approach for production?  

- Named volumes or service-based sharing  

---

### Interview Summary  

“To share data between containers while maintaining isolation, I would use Docker volumes. Multiple containers can mount the same volume, allowing controlled data sharing while keeping the rest of their environments isolated. For more scalable architectures, I would prefer service-based communication like databases or APIs instead of direct file sharing.”

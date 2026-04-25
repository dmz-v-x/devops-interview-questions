### Question  
Your application container loses data when it stops and restarts. How do you fix this?

---

### Answer  

---

### 1. Understanding the Problem

- Docker containers are:
  - **Ephemeral (temporary)**  

- By default:
  - Data is stored in the **container writable layer**  
  - When container is removed → data is lost  

---

### 2. Solution Overview

- Persist data outside the container using:
  - Docker Volumes  
  - Bind Mounts  

---

### 3. Option 1: Docker Volumes (Recommended)

- Managed by Docker  

```bash
docker volume create mydata
```

```bash
docker run -v mydata:/app/data myapp
```

- Behavior:
  - Data stored in `/var/lib/docker/volumes/`  
  - Survives:
    - Container stop  
    - Container deletion  

---

### 4. Option 2: Bind Mounts

- Directly map host directory  

```bash
docker run -v /host/data:/app/data myapp
```

- Behavior:
  - Data stored on host filesystem  
  - Visible and editable outside container  

---

### 5. Real-World Example

- Problem:
  - SQLite DB stored inside container:

```bash
CMD ["sqlite3", "/app/db/mydb.sqlite"]
```

- Fix:

```bash
docker run -v sqlite_data:/app/db my-sqlite-app
```

- Result:
  - Database persists across restarts  

---

### 6. Verify Persistence

```bash
docker stop myapp
docker rm myapp
```

```bash
docker run -v mydata:/app/data myapp
```

- Data will still exist  

---

### 7. Key Takeaways

- Containers are:
  - Temporary by design  

- Always use volumes for:
  - Databases  
  - Logs  
  - User uploads  

- Preferred:
  - Docker volumes over bind mounts (for portability)  

---

### 8. Interview-Ready Summary

“Docker containers are ephemeral, so data stored inside them is lost when they stop or are removed. To fix this, I use Docker volumes or bind mounts to store data outside the container. Volumes are managed by Docker and are preferred for portability, while bind mounts map directly to host directories. This ensures data persists across container restarts.”

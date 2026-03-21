### Question  
If we restart the Docker service using `systemctl restart docker`, will containers keep running or be stopped?

---

### Answer  

### 1. What Happens When Docker Service Restarts  

    sudo systemctl restart docker

---

- Docker daemon stops → all running containers **temporarily stop**  
- Docker daemon starts again → behavior depends on **restart policy**  

---

### 2. Container Behavior After Restart  

| Restart Policy | Behavior After Docker Restart |
|---|---|
| `no` (default) | Container stays **stopped** |
| `always` | Container **restarts automatically** |
| `unless-stopped` | Restarts unless manually stopped |
| `on-failure[:N]` | Restarts only if failed |

---

### 3. Example  

    docker run -d --name myapp --restart always nginx

---

After:

    sudo systemctl restart docker

---

Result:

- Container will **automatically start again**  

---

### 4. Without Restart Policy  

    docker run -d nginx

---

After Docker restart:

- Container will be **stopped**  

---

### 5. Check Container Status  

---

#### All Containers  

    docker ps -a

---

#### Running Containers  

    docker ps

---

### 6. Key Concept  

- Docker does NOT persist running state automatically  
- Restart behavior is controlled by **restart policy**  

---

### 7. Tricky Interview Questions  

---

Do containers run during Docker restart?  

- ❌ No (they stop temporarily)  

---

Do they come back automatically?  

- ✅ Only if restart policy is set  

---

Best restart policy for production?  

- `unless-stopped`  

---

### Interview Summary  

“When the Docker service is restarted, all running containers stop temporarily. After the daemon comes back up, only containers with a restart policy like `always` or `unless-stopped` will automatically restart. Containers without a restart policy will remain in a stopped state.”

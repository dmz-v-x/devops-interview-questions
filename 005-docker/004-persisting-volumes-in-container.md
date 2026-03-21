### Question  
How do you make container volumes persistent, and how do you mount the volume on a custom host directory like `/root/nginx` instead of the default Docker directory?

---

### Answer  

### 1. Why We Need Persistent Volumes  

By default:

- Data inside a container is **ephemeral**  
- When the container is removed → data is lost  

Volumes solve this by storing data **outside the container**, making it persistent.

---

### 2. Types of Docker Volumes  

---

#### Named Volumes  

- Managed by Docker  
- Stored in:

    /var/lib/docker/volumes/

- Example:

    docker run -v myvolume:/data nginx

---

#### Bind Mounts (What We Need Here)  

- Map a **specific host directory** to a container directory  
- Full control over where data is stored  

---

### 3. Mounting a Host Directory (`/root/nginx`)  

---

#### Step 1: Create Host Directory  

    sudo mkdir -p /root/nginx

---

#### Step 2: Run Container with Bind Mount  

    docker run -d \
      --name my-nginx \
      -p 80:80 \
      -v /root/nginx:/usr/share/nginx/html \
      nginx

---

### 4. Explanation  

    -v /root/nginx:/usr/share/nginx/html

| Part | Meaning |
|---|---|
| `/root/nginx` | Host directory |
| `/usr/share/nginx/html` | Container directory |

---

### 5. What Happens Now  

- Any file created inside container path:

        /usr/share/nginx/html

→ gets stored in:

        /root/nginx (host)

---

- If container is deleted:

    docker rm -f my-nginx

✅ Data **still exists** in `/root/nginx`

---

### 6. Verify Volume Mount  

    docker inspect my-nginx

Look for:

    "Mounts": [
      {
        "Type": "bind",
        "Source": "/root/nginx",
        "Destination": "/usr/share/nginx/html"
      }
    ]

---

### 7. Using Docker Compose  

    version: "3.9"
    services:
      web:
        image: nginx
        ports:
          - "80:80"
        volumes:
          - /root/nginx:/usr/share/nginx/html

---

Run:

    docker-compose up -d

---

### 8. Key Concept  

**Container storage vs Volume storage**

| Storage Type | Persistence |
|---|---|
| Container filesystem | ❌ Lost on delete |
| Volume / Bind mount | ✅ Persistent |

---

### 9. Real-World Use Cases  

---

Store website files:

    /root/nginx → HTML files

---

Database storage:

    /data/mysql → persistent DB data

---

Logs storage:

    /var/log/app → survives container restart  

---

---

### 10. Tricky Interview Questions  

---

What is the difference between bind mount and volume?  

| Feature | Bind Mount | Named Volume |
|---|---|---|
| Location | Custom path | Docker-managed |
| Control | Full | Limited |
| Use case | Dev / specific paths | Production |

---

What happens if host directory does not exist?  

- Docker creates it automatically  

---

Can multiple containers share same volume?  

- Yes  

---

Is bind mount safe for production?  

- Less portable, but useful when path control is required  

---

### Interview Summary  

To make container data persistent, use volumes or bind mounts. For storing data in a custom host directory like `/root/nginx`, use a bind mount (`-v host_path:container_path`). This ensures data survives container deletion and is directly accessible on the host system.

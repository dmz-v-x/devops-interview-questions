### Question  
How do you find the IP address of a Docker container?

---

### Answer  

### 1. Using `docker inspect` (Most Common Method)  

Run:

    docker inspect <container-name-or-id>

- Outputs full container details in JSON format  

---

#### Get Only IP Address  

    docker inspect -f '{{ .NetworkSettings.IPAddress }}' <container-name-or-id>

---

#### Example  

    docker inspect -f '{{ .NetworkSettings.IPAddress }}' my-nginx

Output:

    172.17.0.2

---

- This is the container’s **internal IP address**  
- Works for default bridge network  

---

### 2. For User-Defined Networks  

If container is attached to a custom network:

    docker inspect -f '{{ .NetworkSettings.Networks.<network-name>.IPAddress }}' <container-name>

---

#### Example  

    docker inspect -f '{{ .NetworkSettings.Networks.mybridge.IPAddress }}' my-nginx

---

- Replace `mybridge` with your network name  

---

### 3. Using `docker network inspect`  

To view all containers and their IPs on a network:

    docker network inspect <network-name>

---

#### Output Section  

Look under:

    "Containers": {
        "container_id": {
            "Name": "my-nginx",
            "IPv4Address": "172.18.0.2/16"
        }
    }

---

### 4. Key Concept  

- Container IP is **internal to Docker network**  
- Not directly accessible outside unless ports are exposed  

---

### 5. Real-World Notes  

---

Access container via port mapping:

    docker run -p 8080:80 nginx

---

Instead of using IP:

    localhost:8080

---

---

### 6. Tricky Interview Questions  

---

Can container IP change?  

- ✅ Yes (on restart)  

---

Should we rely on container IP in production?  

- ❌ No → use service names or DNS  

---

How do containers communicate?  

- Via Docker network (DNS-based)  

---

Difference between container IP and host IP?  

| Type | Meaning |
|---|---|
| Container IP | Internal Docker network |
| Host IP | Machine IP |

---

### Interview Summary  

You can find a container’s IP address using `docker inspect` with Go templates. For default networks, use `.NetworkSettings.IPAddress`, and for custom networks, use `.NetworkSettings.Networks.<network>.IPAddress`. However, container IPs are dynamic and should not be relied upon in production—use Docker networking and service names instead.

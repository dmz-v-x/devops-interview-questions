### Question  
Our company restricts pulling/pushing from Docker Hub or cloud registries. How can we set up our own local Docker registry and use it?

---

### Answer  

### 1. What is a Docker Registry?  

A **Docker registry** is a server used to:

- Store Docker images  
- Distribute images across systems  

By default:

- `docker pull` / `docker push` → Docker Hub  

But you can run your **own private/local registry**.

---

### 2. Step 1: Run a Local Docker Registry  

Docker provides an official registry image:

    docker run -d -p 5000:5000 --name local-registry registry:2

---

#### Explanation  

| Option | Meaning |
|---|---|
| `-d` | Run in background |
| `-p 5000:5000` | Map host port to container |
| `--name local-registry` | Container name |
| `registry:2` | Official registry image |

---

Now your registry is available at:

    localhost:5000

---

### 3. Step 2: Tag Your Image  

Before pushing, tag your image with registry address:

    docker tag myapp:latest localhost:5000/myapp:latest

---

#### Format  

    <registry-host>:<port>/<image-name>:<tag>

---

### 4. Step 3: Push Image to Local Registry  

    docker push localhost:5000/myapp:latest

---

Now your image is stored in your **local registry**.

---

### 5. Step 4: Pull Image from Local Registry  

    docker pull localhost:5000/myapp:latest

---

- Works on:
  - Same machine  
  - Other machines (if network accessible)

---

### 6. Persist Registry Data (Important)  

By default:

- Registry data is lost if container is deleted  

Fix using bind mount:

    docker run -d -p 5000:5000 \
      --name local-registry \
      -v /root/registry-data:/var/lib/registry \
      registry:2

---

Now:

- Images are stored in:

    /root/registry-data

- Data survives container restart/removal  

---

### 7. Using Docker Compose  

    version: '3'
    services:
      registry:
        image: registry:2
        ports:
          - "5000:5000"
        volumes:
          - /root/registry-data:/var/lib/registry

---

Run:

    docker-compose up -d

---

### 8. Allow Insecure Registry (Without TLS)  

If you don’t use HTTPS, Docker may block it.

Edit:

    /etc/docker/daemon.json

Add:

    {
      "insecure-registries": ["localhost:5000"]
    }

---

Restart Docker:

    sudo systemctl restart docker

---

### 9. Execution Flow  

1. Start registry container  
2. Build your image  
3. Tag image with registry URL  
4. Push image to registry  
5. Pull image when needed  

---

### 10. Real-World Use Cases  

---

Air-gapped environments (no internet)  

---

Internal company deployments  

---

Private CI/CD pipelines  

---

Secure image distribution inside network  

---

---

### 11. Tricky Interview Questions  

---

Where are images stored in local registry?  

- Inside `/var/lib/registry` (or mounted host path)  

---

Why tag image before push?  

- Docker uses tag to determine target registry  

---

Can multiple machines use this registry?  

- Yes, if accessible over network  

---

What happens without persistence?  

- All images are lost when container is removed  

---

Why configure insecure registry?  

- Required when not using HTTPS  

---

### Interview Summary  

You can run your own local Docker registry using the official `registry:2` image. By tagging images with `localhost:5000` and pushing them, you can fully manage images within your network. For production use, persist data with volumes and configure TLS or allow insecure registries if needed.

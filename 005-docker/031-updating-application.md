### Question  
You have a Docker container running a web server, but you need to update the application code inside it. How would you approach this task?

---

### Answer  

### 1. What NOT to Do  

❌ Do NOT update code inside a running container:

    docker exec -it <container> bash

- Containers are **ephemeral**  
- Changes will be lost on restart  
- Not reproducible  

---

### 2. Best Practice: Rebuild the Image  

---

#### Step 1: Update Code  

- Modify application code in your source repository  

---

#### Step 2: Build New Image  

    docker build -t myapp:2.0 .

---

#### Step 3: Replace Container  

    docker stop myapp
    docker rm myapp

---

#### Step 4: Run Updated Container  

    docker run -d -p 80:80 --name myapp myapp:2.0

---

✅ Benefits:

- Version-controlled  
- Reproducible  
- Clean deployment  

---

### 3. Development Approach: Use Volume Mounts  

For frequent code changes:

---

#### Example  

    docker run -d -p 80:80 \
      -v $(pwd)/app:/usr/share/nginx/html \
      --name myapp myapp:dev

---

#### Behavior  

- Code changes on host → reflect instantly in container  

---

⚠️ Use only for development  
❌ Not recommended for production  

---

### 4. Production Approach (CI/CD + Orchestrators)  

---

#### Docker Compose  

    docker-compose up -d --build

---

#### Kubernetes  

    kubectl set image deployment/myapp myapp=myrepo/myapp:2.0

---

#### Flow  

1. Update code  
2. Build image  
3. Push to registry  
4. Deploy new version  

---

### 5. Key Concept  

**Immutable Infrastructure**

- Never modify running containers  
- Always deploy new versions  

---

### 6. Comparison  

| Approach | Use Case | Recommended |
|---|---|---|
| Modify container manually | Quick debug | ❌ No |
| Rebuild image | Production | ✅ Yes |
| Volume mount | Development | ⚠️ Limited |
| CI/CD deployment | Production scale | ✅ Best |

---

### 7. Tricky Interview Questions  

---

Why not edit container directly?  

- Changes are not persistent  

---

What is immutable infrastructure?  

- Replace, don’t modify  

---

How to update zero-downtime?  

- Rolling updates (Kubernetes)  

---

### Interview Summary  

“To update application code in a Docker container, I follow the immutable infrastructure approach. I update the code, rebuild the image, and redeploy the container. For development, I may use volume mounts for quick iteration, but in production, I rely on CI/CD pipelines and orchestration tools to ensure consistent and reliable updates.”

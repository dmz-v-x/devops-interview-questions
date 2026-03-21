### Question  
What is `docker tag`, how does it work, and what is the difference between dangling and unused images?

---

### Answer  

### 1. Docker Tag  

The `docker tag` command is used to create a **new reference (alias)** for an existing image.

---

#### Syntax  

    docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

---

| Part | Meaning |
|---|---|
| SOURCE_IMAGE | Existing image |
| TARGET_IMAGE | New name/tag |
| TAG | Version (default = latest) |

---

### 2. Example  

---

#### Step 1: Check Images  

    docker images

Example:

    REPOSITORY    TAG       IMAGE ID
    myapp         latest    1a2b3c4d5e6f

---

#### Step 2: Tag Image  

    docker tag myapp:latest yourusername/myapp:v1.0

---

#### Step 3: Verify  

    docker images

    REPOSITORY                TAG       IMAGE ID
    myapp                     latest    1a2b3c4d5e6f
    yourusername/myapp        v1.0      1a2b3c4d5e6f

---

✅ Both tags point to the **same IMAGE ID**  
❌ No new image is created  

---

### 3. Tagging for Private Registry  

    docker tag myapp:latest myregistry.example.com/myapp:v1.0

---

- Prepares image for push:

    docker push myregistry.example.com/myapp:v1.0

---

### 4. Common Use Cases  

---

#### Versioning  

    docker tag myapp:latest myapp:v1.1

---

#### Environment Tags  

    docker tag myapp:latest myapp:staging
    docker tag myapp:latest myapp:production

---

#### Docker Hub Push  

    docker tag myapp:latest username/myapp:v1.0

---

### 5. Key Concept  

**Tag = Pointer, NOT a copy**

- Multiple tags → same image  
- Lightweight operation  

---

### 6. Dangling vs Unused Images  

---

| Feature | Dangling Images | Unused Images |
|---|---|---|
| Tagged? | ❌ No (`<none>:<none>`) | ✅ Can be tagged or untagged |
| Used by container? | ❌ No | ❌ No |
| Cause | Rebuilds, intermediate layers | Not referenced by any container |
| Cleanup | `docker image prune` | `docker image prune -a` |

---

### 7. Key Difference  

- **Dangling images** = untagged leftovers  
- **Unused images** = not used, even if tagged  

---

### 8. Cleanup Commands  

---

#### Remove Dangling Images  

    docker image prune

---

#### Remove All Unused Images  

    docker image prune -a

---

⚠️ Warning:

- `-a` removes ALL unused images (even tagged ones)

---

### 9. Tricky Interview Questions  

---

Does `docker tag` create a new image?  

- ❌ No → just adds a reference  

---

Can one image have multiple tags?  

- ✅ Yes  

---

Are all dangling images unused?  

- ✅ Yes  

---

Are all unused images dangling?  

- ❌ No  

---

### Interview Summary  

`docker tag` creates a new reference to an existing image without duplicating it, enabling versioning and registry preparation. Dangling images are untagged leftovers, while unused images are any images not referenced by containers. Proper tagging and cleanup help maintain an efficient Docker environment.

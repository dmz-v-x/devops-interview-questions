### Question  
What is `docker commit`? Should the container be running or stopped when committing? Explain everything with an example in simple terms.

---

### Answer  

### 1. What is Docker Commit?  

`docker commit` is used to **create a new image from an existing container**.

---

#### Simple Meaning  

👉 Think of it like:

- You start a container  
- Make changes (install software, create files)  
- Then **take a snapshot**  

That snapshot = **new Docker image**

---

### 2. What Gets Saved?  

✔ Filesystem changes  
❌ Running processes  

---

Example:

- Installed packages → saved  
- Created files → saved  
- Running app → NOT saved  

---

### 3. Running vs Stopped Container  

---

#### Case 1: Running Container  

    docker commit <container> myimage:v1

- Takes snapshot of current state  
- Includes all changes so far  

⚠️ Risk:

- Data may be inconsistent if app is writing files  

---

#### Case 2: Stopped Container (Recommended)  

    docker commit <container> myimage:v1

- Snapshot is stable  
- No active writes  

✅ Best practice → **commit stopped container**

---

### 4. Basic Syntax  

    docker commit [OPTIONS] <container> <image>:<tag>

---

### 5. Step-by-Step Example  

---

#### Step 1: Run Container  

    docker run -it ubuntu bash

---

#### Step 2: Make Changes  

Inside container:

    apt update
    apt install -y curl
    echo "Hello Docker" > /hello.txt
    exit

---

Now container is **stopped**

---

#### Step 3: Commit Container  

    docker ps -a

Find container ID, then:

    docker commit <container-id> myubuntu:custom

---

### 6. Verify New Image  

    docker images

---

You’ll see:

    myubuntu   custom

---

### 7. Run New Container  

    docker run -it myubuntu:custom bash

---

Check:

    cat /hello.txt

Output:

    Hello Docker

---

✔ Changes are preserved  

---

### 8. Add Metadata (Optional)  

    docker commit -m "Installed curl" -a "Himanshu" <container-id> myubuntu:custom

---

| Option | Meaning |
|---|---|
| `-m` | Message |
| `-a` | Author |

---

### 9. Key Concepts  

---

#### Commit = Snapshot  

- Saves container state as image  

---

#### Immutable Images  

- Original image unchanged  

---

#### No Process State  

- Only filesystem saved  

---

### 10. When to Use docker commit  

---

#### Good Use Cases  

- Quick debugging  
- Experimentation  
- Learning  

---

#### Not Recommended For  

- Production builds  

👉 Use **Dockerfile instead**

---

### 11. Tricky Interview Questions  

---

Does commit save running processes?  

- ❌ No  

---

Can you commit a running container?  

- ✅ Yes (but risky)  

---

Best practice?  

- Commit stopped container  

---

Difference: commit vs Dockerfile?  

| Feature | Commit | Dockerfile |
|---|---|---|
| Reproducible | ❌ No | ✅ Yes |
| Use case | Debugging | Production |

---

### Interview Summary  

“`docker commit` creates a new image from a container’s current state. It can be done on both running and stopped containers, but it’s safer to commit a stopped container to ensure consistency. It saves filesystem changes but not running processes. In practice, it’s mainly used for debugging, while Dockerfiles are preferred for production workflows.”

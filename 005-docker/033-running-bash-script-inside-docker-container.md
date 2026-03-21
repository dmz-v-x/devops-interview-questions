### Question  
You created a bash script on your local machine and want to run it inside a Docker container. How can you do it?

---

### Answer  

### 1. Copy Script into Container (Most Common)  

---

#### Step 1: Copy Script  

    docker cp /path/to/local/script.sh <container-name>:/tmp/script.sh

---

#### Step 2: Execute Script  

    docker exec -it <container-name> bash /tmp/script.sh

---

✅ Best for:

- Running scripts on existing containers  
- One-time execution  

---

### 2. Mount Script Using Volume (Best for Development)  

---

#### Run Container with Script  

    docker run -v /path/to/local/script.sh:/tmp/script.sh -it <image> bash /tmp/script.sh

---

#### Explanation  

| Part | Meaning |
|---|---|
| `/local/script.sh` | Your local file |
| `/tmp/script.sh` | Inside container |

---

✅ Benefits:

- No need to copy  
- Live updates reflect instantly  

---

⚠️ Limitation:

- Works best when starting container  
- Not ideal for already running containers  

---

### 3. Use Input Redirection (Quickest Way)  

---

    docker exec -i <container-name> bash < /path/to/local/script.sh

---

#### How It Works  

- Sends script as input to bash  
- No copy, no mount  

---

✅ Best for:

- Quick execution  
- Temporary tasks  

---

### 4. Best Practice Summary  

| Method | Use Case | Recommended |
|---|---|---|
| docker cp + exec | Production/debug | ✅ Yes |
| Volume mount | Development | ✅ Yes |
| Input redirection | Quick run | ⚠️ Limited |

---

### 5. Key Concept  

- Containers are **isolated environments**  
- You must:
  - Copy  
  - Mount  
  - Or stream data  

---

### 6. Tricky Interview Questions  

---

Does script persist after container restart?  

- Only if copied or baked into image  

---

Best way for permanent scripts?  

- Add to Dockerfile  

---

Can you mount file into running container?  

- ❌ Not directly (requires restart)  

---

### Interview Summary  

“To run a local script inside a container, I can copy it using `docker cp` and execute it with `docker exec`, or mount it using volumes for development. For quick execution, I can pipe the script using input redirection. In production, I prefer baking scripts into the Docker image for consistency.”

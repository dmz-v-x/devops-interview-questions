### Question  
Why does an Ubuntu container often exit immediately, while images like nginx or mysql usually keep running?

---

### Answer  

### 1. Why Ubuntu Container Exits Immediately  

When you run:

    docker run ubuntu

Docker starts the container and executes the default command defined in the image.

For the Ubuntu image, the default is:

    CMD ["bash"]

However:

- `bash` requires an **interactive terminal**  
- If no terminal is attached, `bash` starts and exits immediately  

So the container:

1. Starts  
2. Runs `bash`  
3. Exits instantly → container stops  

---

#### Fix (Run Interactively)  

    docker run -it ubuntu

- `-i` → interactive mode  
- `-t` → allocates a terminal  

Now:

- Bash stays open  
- Container remains running  

---

### 2. Why nginx / mysql Containers Keep Running  

These images are designed to run **long-lived processes**.

---

#### nginx  

Default command:

    nginx -g "daemon off;"

- Runs nginx in **foreground mode**  
- Does NOT exit  
- Keeps container alive  

---

#### mysql  

Default command:

    mysqld

- Starts MySQL server  
- Runs continuously  
- Keeps container alive  

---

### 3. Key Concept (Most Important)  

A Docker container lives and dies with its **main process (PID 1)**.

- If the main process exits → container stops  
- If the main process keeps running → container stays alive  

---

### 4. Mental Model  

Think of a container as:

    Container = Process

NOT:

    Container = VM

---

| Image | Main Process | Behavior |
|---|---|---|
| ubuntu | bash | Exits immediately (no terminal) |
| nginx | nginx (foreground) | Keeps running |
| mysql | mysqld | Keeps running |

---

### 5. How to Keep Any Container Running  

---

#### Option 1: Interactive Mode  

    docker run -it ubuntu

---

#### Option 2: Run a Long Process  

    docker run ubuntu sleep 1000

---

#### Option 3: Infinite Loop  

    docker run ubuntu tail -f /dev/null

---

### 6. Tricky Interview Questions  

---

Why does container stop after script finishes?  

- Because the main process exits  

---

What is PID 1 in a container?  

- The first process started (controls container lifecycle)  

---

Why use `daemon off` in nginx?  

- Prevents backgrounding → keeps process in foreground  

---

Difference between VM and container lifecycle?  

| VM | Container |
|---|---|
| Runs OS | Runs process |
| Always running | Stops when process exits |

---

### Interview Summary  

Ubuntu containers exit immediately because their default command (`bash`) finishes when no terminal is attached. In contrast, nginx and mysql run long-lived foreground processes, keeping the container alive. The key rule is: **a container runs as long as its main process is running**.

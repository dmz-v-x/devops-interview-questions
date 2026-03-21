### Question  
How can you make a Docker container restart automatically when the Docker service restarts?

---

### Answer  

### 1. Use `--restart` Flag  

Docker provides a **restart policy** using the `--restart` flag.

---

#### Syntax  

    docker run --restart <policy> <image>

---

### 2. Available Restart Policies  

| Policy | Description |
|---|---|
| `no` (default) | Do not restart |
| `always` | Always restart (even after Docker daemon restart) |
| `unless-stopped` | Restart unless manually stopped |
| `on-failure[:N]` | Restart only on failure (optional retry limit) |

---

### 3. Example (Auto Restart on Docker Restart)  

    docker run -d --name mynginx --restart always nginx

---

#### Explanation  

| Option | Meaning |
|---|---|
| `-d` | Run in background |
| `--restart always` | Enable auto-restart |
| `nginx` | Image |

---

### 4. Behavior of `--restart=always`  

| Event | Behavior |
|---|---|
| Container crashes | Restarted automatically |
| Docker service restarts | Restarted automatically |
| Manual `docker stop` | Not restarted |

---

### 5. Update Existing Container  

If container already exists:

    docker update --restart=always <container-name>

---

- No need to recreate container  
- Applies restart policy instantly  

---

### 6. Best Practice  

- Use:

    --restart unless-stopped

---

#### Why?  

- Prevents restart after manual stop  
- Still restarts on daemon reboot  

---

### 7. Key Concept  

- Restart policy is managed by **Docker daemon**  
- Ensures **high availability** of containers  

---

### 8. Tricky Interview Questions  

---

Difference between `always` and `unless-stopped`?  

| Policy | Behavior |
|---|---|
| always | Always restart (even after stop) |
| unless-stopped | Respect manual stop |

---

Does restart policy work if container is removed?  

- ❌ No  

---

Does it restart failed containers?  

- ✅ Yes (depending on policy)  

---

### Interview Summary  

“To ensure containers restart automatically when Docker restarts, I use the `--restart` flag, typically `--restart=always` or `unless-stopped`. This ensures containers recover automatically after crashes or daemon restarts, improving reliability and availability.”

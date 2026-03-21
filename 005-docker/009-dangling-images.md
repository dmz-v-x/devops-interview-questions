### Question  
What are dangling images in Docker?

---

### Answer  

### 1. Definition  

A **dangling image** is a Docker image that:

- Has **no tag** (`<none>:<none>`)  
- Is **not referenced by any container**  

These images are essentially **unused intermediate layers** left behind during image operations.

---

### 2. How Dangling Images Appear  

Run:

    docker images -a

Example output:

    REPOSITORY    TAG       IMAGE ID     CREATED        SIZE
    <none>        <none>    abc123       2 days ago     150MB
    <none>        <none>    def456       3 days ago     200MB
    ubuntu        latest    7e0aa2d69a1f 2 weeks ago    72MB

---

- Images with:

        <none> : <none>

→ are **dangling images**

---

### 3. Why Dangling Images Are Created  

---

#### Rebuilding Images  

    docker build -t myapp .

- Old layers become unused  
- New image replaces them  
- Old layers become dangling  

---

#### Image Updates / Pulls  

- New version pulled  
- Old layers remain unreferenced  

---

#### Retagging Images  

    docker tag myapp newname

- Old tag removed → image becomes untagged  

---

### 4. Why They Matter  

---

#### Disk Space Waste  

- Consume storage unnecessarily  

---

#### Clutter  

- Makes `docker images` output messy  

---

#### Maintenance Overhead  

- Need periodic cleanup  

---

### 5. How to Manage Dangling Images  

---

#### List Dangling Images  

    docker images -f dangling=true

---

#### Remove Dangling Images  

    docker image prune

- Removes all dangling images  

---

#### Remove All Unused Images  

    docker system prune -a

⚠️ Warning:

- Removes:
  - Unused images  
  - Stopped containers  
  - Networks  

---

### 6. Key Concept  

**Dangling ≠ Unused Image (Always)**  

| Type | Meaning |
|---|---|
| Dangling image | Untagged (`<none>`) |
| Unused image | Not used by any container |

---

### 7. Tricky Interview Questions  

---

Are dangling images used by containers?  

- No  

---

Can tagged images be unused?  

- Yes  

---

Is it safe to delete dangling images?  

- Yes, generally safe  

---

Difference between `prune` and `system prune -a`?  

| Command | Scope |
|---|---|
| `docker image prune` | Only dangling images |
| `docker system prune -a` | All unused resources |

---

### Interview Summary  

Dangling images are untagged (`<none>:<none>`) Docker images that are not used by any container. They are typically created during rebuilds or updates and can consume unnecessary disk space. They can be safely removed using `docker image prune` to keep the system clean and efficient.

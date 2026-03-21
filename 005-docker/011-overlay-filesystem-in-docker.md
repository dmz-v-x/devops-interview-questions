### Question  
What is the Overlay filesystem in Docker, and what is the Overlay driver?

---

### Answer  

### 1. Overlay Filesystem  

#### Definition  

The **Overlay filesystem** is a **union filesystem** used by Docker to combine multiple layers into a single unified view.

It allows:

- Read-only image layers  
- A writable container layer  

to appear as **one filesystem** inside the container.

---

### 2. How It Works  

Docker images are built in **layers**.

When a container runs:

- Base image layers → **read-only**  
- Container layer → **read-write**  

---

#### Structure  

    Image Layer 3 (read-only)
    Image Layer 2 (read-only)
    Image Layer 1 (read-only)
    -------------------------
    Container Layer (read-write)

---

#### Unified View  

The container sees:

    / (single merged filesystem)

---

### 3. Copy-on-Write (CoW) Concept  

Overlay uses **Copy-on-Write**:

- If a file is NOT modified → use existing layer  
- If modified:
  - File is copied to writable layer  
  - Changes happen there  

---

#### Example  

- File exists in image layer  
- Container modifies it  

→ Copy is created in container layer  
→ Original image remains unchanged  

---

### 4. Key Features  

---

#### Efficient Storage  

- Layers are shared across containers  
- No duplication of unchanged data  

---

#### Fast Container Startup  

- No need to copy entire filesystem  

---

#### Layered Architecture  

- Each Dockerfile step = new layer  

---

### 5. Overlay Driver (overlay2)  

#### Definition  

The **Overlay driver** is the Docker **storage driver** that implements the overlay filesystem.

---

#### Purpose  

- Manages:
  - Image layers  
  - Container writable layers  
- Handles:
  - Copy-on-write  
  - Layer merging  

---

### 6. overlay2 (Modern Standard)  

- Default storage driver on most Linux systems  
- Improved performance over older drivers  

---

#### Check Storage Driver  

    docker info | grep "Storage Driver"

Example:

    Storage Driver: overlay2

---

### 7. Other Storage Drivers  

| Driver | Status |
|---|---|
| overlay2 | Recommended |
| aufs | Deprecated |
| devicemapper | Legacy |
| btrfs / zfs | Advanced use cases |

---

### 8. Internal Working (Simplified)  

Overlay uses:

- **Lowerdir** → image layers (read-only)  
- **Upperdir** → container layer (write)  
- **Workdir** → internal operations  

Merged as:

- **Merged directory** → visible to container  

---

### 9. Benefits  

---

#### Space Efficiency  

- Shared layers reduce disk usage  

---

#### Performance  

- Faster builds and container startup  

---

#### Isolation  

- Changes don’t affect base images  

---

### 10. Tricky Interview Questions  

---

What happens when a file is modified?  

- Copied to writable layer (CoW)  

---

Do containers share image layers?  

- Yes  

---

Does modifying a container change the image?  

- No  

---

Why is overlay2 preferred?  

- Better performance and stability  

---

### Interview Summary  

The Overlay filesystem is a union filesystem that merges multiple read-only image layers with a writable container layer into a single view. The Overlay driver (`overlay2`) is Docker’s storage driver that implements this mechanism, enabling efficient storage, fast performance, and copy-on-write behavior.

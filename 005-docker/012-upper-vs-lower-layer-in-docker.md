### Question  
What are the upper layer and lower layer in Docker’s overlay filesystem architecture? Explain from scratch.

---

### Answer  

### 1. What is Overlay Filesystem?  

The **Overlay filesystem** is a type of **union filesystem** used by Docker to combine multiple layers into a **single unified view**.

Think of it like stacking transparent sheets:

- Each sheet = a layer  
- Final view = combination of all layers  

---

#### Key Concept: Copy-on-Write (CoW)  

- Files are NOT copied unless modified  
- Only changes are stored separately  

---

### 2. Docker Image Layers (Foundation)  

Docker images are built in **layers**.

Example Dockerfile:

    FROM ubuntu:20.04
    RUN apt-get update
    RUN apt-get install -y nginx
    COPY index.html /var/www/html/

---

#### Layers Created  

| Layer | Description |
|---|---|
| Layer 1 | Base OS (Ubuntu) |
| Layer 2 | apt-get update |
| Layer 3 | Install nginx |
| Layer 4 | Copy file |

---

✅ All these layers are **read-only**

---

### 3. Overlay Architecture (Core Idea)  

Overlay filesystem combines:

- Lower layers (read-only)  
- Upper layer (read-write)  

to create a:

- Merged layer (what container sees)

---

### 4. Lower Layer (lowerdir)  

#### Definition  

The **lower layer** is a stack of **read-only image layers**.

---

#### Characteristics  

- Immutable (cannot be changed)  
- Shared across multiple containers  
- Contains:
  - OS files  
  - Installed packages  
  - App code from image  

---

#### Example  

    ubuntu layer
    + nginx installed
    + app files

---

### 5. Upper Layer (upperdir)  

#### Definition  

The **upper layer** is the **writable layer** created for each container.

---

#### Characteristics  

- Unique per container  
- Stores:
  - Modified files  
  - New files  
  - Deleted file markers  

---

#### Example  

    /var/www/html/index.html  (new file)
    /etc/nginx/nginx.conf     (modified file)

---

### 6. Merged Layer (mergeddir)  

#### Definition  

The **merged layer** is the **final combined view** of:

    lower layers + upper layer

---

#### What Container Sees  

- A single filesystem (`/`)  
- Does NOT see layers separately  

---

### 7. How Copy-on-Write Works  

---

#### Case 1: Reading a File  

1. Check upper layer  
2. If not found → check lower layers  

---

#### Case 2: Modifying a File  

1. File exists in lower layer  
2. Copy it to upper layer  
3. Modify it there  

---

#### Case 3: Creating a File  

- Directly created in upper layer  

---

#### Case 4: Deleting a File  

- A **whiteout file** is created in upper layer  
- Hides file from lower layers  

---

### 8. Visual Representation  

    Lower Layer 3 (read-only)
    Lower Layer 2 (read-only)
    Lower Layer 1 (read-only)
    ----------------------------
    Upper Layer (read-write)
    ----------------------------
    Merged View (container sees this)

---

### 9. Real Example  

---

#### Image Layers  

- Ubuntu  
- Nginx installed  

---

#### Container Changes  

- Modify nginx config  
- Add HTML file  

---

#### Storage  

- Original files → remain in lower layers  
- Changes → stored in upper layer  

---

### 10. Key Terms  

| Term | Meaning |
|---|---|
| Lower Layer | Read-only image layers |
| Upper Layer | Writable container layer |
| Merged Layer | Combined filesystem view |
| Whiteout File | Marks deletion of lower-layer file |

---

### 11. Advantages  

---

#### Efficient Storage  

- Multiple containers share same lower layers  

---

#### Isolation  

- Each container has its own upper layer  

---

#### Immutability  

- Base image never changes  

---

#### Fast Startup  

- No need to copy full filesystem  

---

### 12. Tricky Interview Questions  

---

Can containers modify image layers?  

- ❌ No  

---

Where are changes stored?  

- Upper layer  

---

Do containers share upper layer?  

- ❌ No (each container has its own)  

---

Do containers share lower layers?  

- ✅ Yes  

---

What happens when container is deleted?  

- Upper layer is deleted  
- Lower layers remain  

---

### Interview Summary  

In Docker’s overlay filesystem, the **lower layers** are read-only image layers shared across containers, while the **upper layer** is a writable layer unique to each container. These layers are merged into a single filesystem view using copy-on-write, enabling efficient storage, isolation, and fast container execution.

### Question  
What are image layer (lowerdir), container layer (upperdir), and container mount (merged) in OverlayFS (Docker)?

---

### Answer  

### 1. Overview of OverlayFS in Docker  

Docker uses **OverlayFS** (via `overlay2` driver) to manage images and containers efficiently.

It combines:

- Read-only image layers  
- A writable container layer  

into a **single unified filesystem view**.

---

### 2. Image Layer (`lowerdir`)  

#### Definition  

`lowerdir` represents the **read-only layers of a Docker image**.

These are all the layers created during image build.

---

#### Characteristics  

| Feature | Description |
|---|---|
| Type | Read-only |
| Shared | Yes (across containers) |
| Contains | OS, libraries, app code |

---

#### Example  

    Layer1: Ubuntu base
    Layer2: Installed packages
    Layer3: Application code

---

✅ Cannot be modified  
✅ Shared across multiple containers  

---

### 3. Container Layer (`upperdir`)  

#### Definition  

`upperdir` is the **writable layer created for each container**.

---

#### Characteristics  

| Feature | Description |
|---|---|
| Type | Writable |
| Unique | Yes (per container) |
| Stores | Changes, new files, deletions |

---

#### What Goes Here  

- Modified files  
- Newly created files  
- Whiteout files (for deletions)  

---

#### Example  

    /app/config.json     (new file)
    /etc/nginx.conf     (modified file)

---

### 4. Container Mount (`merged`)  

#### Definition  

`merged` is the **combined view of lowerdir + upperdir**.

---

#### What Container Sees  

- A single filesystem (`/`)  
- Does NOT see layers separately  

---

#### Characteristics  

| Feature | Description |
|---|---|
| Type | Virtual combined view |
| Visible to | Container |
| Read | upperdir → fallback to lowerdir |
| Write | Always to upperdir |

---

### 5. How They Work Together (COW)  

---

#### Structure  

    lowerdir (read-only layers)
    ---------------------------
    upperdir (writable layer)
    ---------------------------
    merged (final view)

---

#### Scenario  

File exists in image:

    /etc/config.yaml  (in lowerdir)

---

##### When container reads  

- Looks in upperdir  
- If not found → reads from lowerdir  

---

##### When container modifies  

1. File copied from lowerdir → upperdir  
2. Modification happens in upperdir  

---

##### When container deletes  

- A **whiteout file** is created in upperdir  
- File is hidden from merged view  

---

### 6. Visual Flow  

    Lower Layers (lowerdir)
    - Ubuntu
    - Dependencies
    - App files

    -------------------------

    Upper Layer (upperdir)
    - Modified config
    - New files

    -------------------------

    Merged View (container sees)
    - Combined filesystem

---

### 7. Advantages  

---

#### Space Efficiency  

- Lower layers shared across containers  

---

#### Fast Startup  

- No full filesystem copy  

---

#### Isolation  

- Each container has its own upperdir  

---

#### Immutability  

- Image layers never change  

---

### 8. Key Summary Table  

| OverlayFS Component | Role |
|---|---|
| `lowerdir` | Read-only image layers |
| `upperdir` | Writable container layer |
| `merged` | Combined filesystem view |

---

### 9. Tricky Interview Questions  

---

Where are changes stored?  

- In `upperdir`  

---

Can lowerdir be modified?  

- ❌ No  

---

Do containers share upperdir?  

- ❌ No  

---

Do containers share lowerdir?  

- ✅ Yes  

---

What does container actually see?  

- `merged` view  

---

### Interview Summary  

In Docker’s OverlayFS, `lowerdir` contains shared read-only image layers, `upperdir` is the container’s writable layer storing all changes, and `merged` is the unified filesystem presented to the container. Together, they enable efficient storage, isolation, and copy-on-write behavior.

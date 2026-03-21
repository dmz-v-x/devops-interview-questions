### Question  
What is the parent-child relationship between Docker images, and how do you find the parent and child images?

---

### Answer  

### 1. What is Parent-Child Relationship in Docker Images?  

Docker images are built using **layers**.

When you create an image using a Dockerfile:

    FROM ubuntu:20.04
    RUN apt update && apt install -y curl

---

#### Relationship  

- `ubuntu:20.04` → **Parent Image**  
- New image (with curl) → **Child Image**  

---

### 2. Key Concept  

- Each instruction in Dockerfile = new layer  
- Child image = parent image + new layers  
- Parent image remains unchanged (immutable)  

---

### 3. Visual Representation  

    Parent Image (ubuntu:20.04)
    ----------------------------
    Child Layer (install curl)
    ----------------------------
    Final Image (myubuntu:custom)

---

### 4. List Images  

    docker images

---

#### Example  

    REPOSITORY   TAG       IMAGE ID
    myubuntu     custom    abc123
    ubuntu       20.04     def456

---

- `myubuntu:custom` → child  
- `ubuntu:20.04` → parent  

---

### 5. Find Parent Image  

---

#### Using Inspect  

    docker inspect myubuntu:custom

---

Look for:

    "Parent": "sha256:def456..."

---

- This shows parent image ID  

---

### 6. Check Layers (RootFS)  

    docker inspect myubuntu:custom

---

Look for:

    "RootFS": {
      "Layers": [
        "sha256:parent-layer",
        "sha256:child-layer"
      ]
    }

---

- First layers → parent  
- Last layer → child  

---

### 7. Find Parent-Child Mapping  

---

#### Command  

    docker inspect --format='{{.Id}} -> {{.Parent}}' $(docker images -q)

---

#### Example Output  

    sha256:abc123 -> sha256:def456
    sha256:def456 -> <none>

---

- `<none>` → base image (no parent)  
- Others → child → parent mapping  

---

### 8. Find Child Images (Indirect Way)  

Docker doesn’t provide a direct command.

---

#### Approach  

- List all images  
- Match `.Parent` field  

---

### 9. Key Points  

---

- Parent image = base layer  
- Child image = extended version  
- Images share layers → saves space  

---

### 10. Tricky Interview Questions  

---

Does modifying child image affect parent?  

- ❌ No  

---

Can one parent have multiple children?  

- ✅ Yes  

---

What is root image?  

- Image with no parent (`<none>`)  

---

How are layers reused?  

- Via content hashing  

---

### Interview Summary  

In Docker, images follow a parent-child relationship where a child image is built on top of a parent image by adding new layers. You can identify the parent using `docker inspect` and examining the `Parent` field or image layers. This layered architecture enables efficient storage and reuse across images.

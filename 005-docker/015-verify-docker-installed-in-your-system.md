### Question  
How do you verify where Docker is installed on your machine, and what is the file path where Docker stores its data?

---

### Answer  

### 1. Check Docker Binary Path  

To find where the Docker executable is installed:

    which docker

---

#### Example Output  

    /usr/bin/docker

---

#### Alternative  

    type -a docker

- Shows all locations of the `docker` command in your `$PATH`

---

### 2. Verify Docker Installation  

    docker version

- Confirms:
  - Docker is installed  
  - Docker daemon is running  
- Also shows client and server versions  

---

### 3. Check Docker Storage Path (Important)  

Docker stores all its data (images, containers, volumes) in a directory called:

    /var/lib/docker

---

#### Verify Using Command  

    docker info | grep "Docker Root Dir"

---

#### Example Output  

    Docker Root Dir: /var/lib/docker

---

### 4. What is Stored Inside `/var/lib/docker`  

---

| Directory | Purpose |
|---|---|
| overlay2 | Image layers (OverlayFS) |
| containers | Container metadata/logs |
| volumes | Persistent volumes |
| image | Image metadata |
| network | Network configuration |

---

### 5. Custom Docker Data Directory  

Docker can be configured to use a different storage path.

---

#### Check Configuration  

    cat /etc/docker/daemon.json

---

#### Example  

    {
      "data-root": "/mnt/docker-data"
    }

---

#### Meaning  

- Docker will store everything in:

        /mnt/docker-data

instead of:

        /var/lib/docker

---

### 6. Key Concept  

- `/usr/bin/docker` → Docker CLI binary  
- `/var/lib/docker` → Docker **data directory**  

---

### 7. Tricky Interview Questions  

---

Is `/usr/bin/docker` the main Docker process?  

- ❌ No → it's just the CLI  

---

Where does Docker store images?  

- `/var/lib/docker/overlay2/`  

---

Can we change Docker data directory?  

- ✅ Yes (via `daemon.json`)  

---

What happens if `/var/lib/docker` is deleted?  

- ❌ All containers, images, volumes are lost  

---

### Interview Summary  

Docker’s executable is typically located at `/usr/bin/docker`, while all Docker data (images, containers, volumes) is stored under `/var/lib/docker` by default. This location can be verified using `docker info` and customized using the Docker daemon configuration.

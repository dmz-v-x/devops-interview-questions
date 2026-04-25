### Question  
Python script to run a container using Docker SDK - User provides image name as input

---

### Answer  

---

### 1. Overview

- Goal:
  - Take Docker image name as input  
  - Pull image if not present  
  - Run container using Docker SDK  

- Requirement:
  - Docker installed  
  - User has permission to access Docker daemon  

---

### 2. Python Script

```python
import docker

# Initialize Docker client
client = docker.from_env()

# Get image name from user input
image_name = input("Enter the Docker image name (e.g., nginx:latest): ").strip()

try:
    # Pull the image (if not present locally)
    print(f"Pulling image '{image_name}'...")
    client.images.pull(image_name)
    print(f"Image '{image_name}' pulled successfully.")

    # Run the container
    print(f"Running container from image '{image_name}'...")
    container = client.containers.run(image_name, detach=True)

    print(f"Container started with ID: {container.id[:12]}")

except docker.errors.ImageNotFound:
    print(f"Error: Image '{image_name}' not found.")
except docker.errors.APIError as e:
    print(f"Docker API error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

---

### 3. How It Works

- `docker.from_env()`  
  - Connects to local Docker engine  

- `client.images.pull()`  
  - Downloads image if not present  

- `client.containers.run()`  
  - Starts container  
  - `detach=True` → runs in background  

---

### 4. Example Usage

```bash
python run_container.py
```

Input:

```
Enter the Docker image name (e.g., nginx:latest): alpine
```

Output:

```
Pulling image 'alpine'...
Image 'alpine' pulled successfully.
Running container from image 'alpine'...
Container started with ID: 3e1fabc2d789
```

---

### 5. Enhancements (Best Practices)

- Add port mapping:

```python
client.containers.run(image_name, detach=True, ports={'80/tcp': 8080})
```

- Add container name:

```python
client.containers.run(image_name, name="my_container", detach=True)
```

- Add environment variables:

```python
client.containers.run(image_name, detach=True, environment={"ENV": "prod"})
```

---

### 6. Key Takeaways

- Docker SDK allows:
  - Programmatic container management  

- Useful for:
  - Automation  
  - CI/CD pipelines  

---

### 7. Interview-Ready Summary

“I can use the Docker Python SDK to programmatically run containers by connecting to the Docker daemon using docker.from_env(), pulling the image if needed, and starting a container using client.containers.run(). This is useful for automation and integrating Docker operations into scripts or CI/CD pipelines.”

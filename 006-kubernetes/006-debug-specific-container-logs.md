### Question  
How to debug specific container logs when there are multiple containers inside a single Pod?

---

### Answer  

### 1. List Pods  

Start by identifying the Pod:

    kubectl get pods

---

### 2. Check Container Names Inside the Pod  

Find all containers in the Pod:

    kubectl describe pod <pod-name>

Look for:

    Containers:
      myapp
      log-shipper

- These names are required to fetch logs  

---

### 3. View Logs of a Specific Container  

Use the `-c` flag:

    kubectl logs <pod-name> -c <container-name>

Example:

    kubectl logs mypod -c myapp
    kubectl logs mypod -c log-shipper

- Helps debug each container independently  

---

### 4. Stream Logs in Real-Time  

    kubectl logs -f <pod-name> -c <container-name>

- `-f` (follow) shows live logs  

---

### 5. Debug Crashed Container Logs  

If container restarted:

    kubectl logs <pod-name> -c <container-name> --previous

- Shows logs from the **previous crashed instance**  

---

### 6. Quick Summary  

| Command                                  | Use Case                                     |
|------------------------------------------|----------------------------------------------|
| `kubectl logs <pod>`                     | Single-container Pod logs                    |
| `kubectl logs <pod> -c <container>`      | Logs for specific container                 |
| `kubectl logs -f <pod> -c <container>`   | Live streaming logs                         |
| `kubectl logs -c <container> --previous` | Logs from previous (crashed) container      |

---

### 7. Key Insight  

- Pods can have multiple containers  
- Logs are **container-specific**, not Pod-wide by default  

---

### Interview Summary  

To debug logs in a multi-container Pod, first identify container names using `kubectl describe pod`, then use `kubectl logs <pod> -c <container>` to fetch logs for a specific container, with options like `-f` for streaming and `--previous` for crashed instances.

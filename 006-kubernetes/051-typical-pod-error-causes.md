### Question  
Name three typical Pod error causes and how they can be fixed.

---

### Answer  

### 1. Image Pull Errors  

---

#### Cause  

- Incorrect image name or tag  
- Missing registry credentials  
- Network issues  

---

#### Symptoms  

- Status: ImagePullBackOff / ErrImagePull  

---

#### Fix  

- Verify image name & tag  
- Add registry credentials  

Example:

    imagePullSecrets:
      - name: myregistrykey

- Check details:

    kubectl describe pod <pod-name>

---

### 2. CrashLoopBackOff (Application Crash)  

---

#### Cause  

- App crashes after start  

Common reasons:

- Wrong environment variables  
- Missing dependencies  
- Runtime errors  

---

#### Symptoms  

- Pod keeps restarting  
- CrashLoopBackOff status  

---

#### Fix  

- Check logs:

    kubectl logs <pod-name>

- Fix:

  - Configuration  
  - Dependencies  
  - Code issues  

- Ensure:

  - ConfigMaps/Secrets mounted  
  - Probes configured  

---

### 3. Insufficient Resources / Scheduling Issues  

---

#### Cause  

- Not enough CPU/memory  
- Node constraints (taints, affinity)  

---

#### Symptoms  

- Pod stuck in Pending  

Message:

    0/3 nodes are available: Insufficient cpu/memory

---

#### Fix  

- Check nodes:

    kubectl describe nodes

- Adjust resources:

    resources:
      requests:
        cpu: "200m"
        memory: "256Mi"
      limits:
        cpu: "500m"
        memory: "512Mi"

- Or:

  - Add more nodes  
  - Fix taints/tolerations  

---

### 4. Summary  

| Error Type               | Symptoms              | Fix                                      |
|--------------------------|----------------------|------------------------------------------|
| ImagePullBackOff         | Cannot pull image     | Fix image name or credentials            |
| CrashLoopBackOff         | Continuous restart    | Check logs, fix app/config               |
| Pending (resources)      | Not scheduled         | Adjust resources or scale cluster        |

---

### 5. Key Insight  

- Most pod issues fall into:

  - Image  
  - Application  
  - Resources  

---

### Interview Summary  

Common pod failures in Kubernetes include image pull errors, application crashes (CrashLoopBackOff), and scheduling issues due to insufficient resources. These can be resolved by verifying image configurations, debugging application logs, and ensuring proper resource allocation and cluster capacity.

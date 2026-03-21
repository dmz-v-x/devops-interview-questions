### Question  
Recently created Nginx Pod status is Pending. Find out why?

---

### Answer  

### 1. Check Pod Details  

Start with:

    kubectl describe pod <nginx-pod-name>

Focus on the **Events section** at the bottom.

Look for messages like:

    0/3 nodes are available: <reason>  
    FailedScheduling  

These messages directly tell you **why the Pod is stuck in Pending**.

---

### 2. Common Reasons for Pending Status  

---

#### a) Not Enough Resources  

- Node does not have enough **CPU / Memory**  

Example:

    0/3 nodes are available: 1 Insufficient cpu, 2 Insufficient memory

Fix:

- Reduce resource requests in Pod  
- Add more nodes  
- Increase node capacity  

---

#### b) NodeSelector / Taints / Tolerations Issues  

Pod may be restricted to specific nodes:

    nodeSelector:
      disktype: ssd

Or nodes may be tainted:

    NoSchedule taint present

Example:

    0/3 nodes are available: 3 node(s) didn't match node selector

Fix:

- Add correct labels to nodes  
- Remove taints OR add tolerations  

---

#### c) PersistentVolumeClaims (PVC) Not Bound  

If Pod is using a volume and PVC is not bound:

Example:

    pod has unbound PersistentVolumeClaims

Fix:

- Create a matching PersistentVolume (PV)  
- Check StorageClass configuration  

---

#### d) Image Pull Issues  

Kubernetes cannot pull the container image.

Example:

    Failed to pull image "nginx": rpc error: code = Unknown desc = ...

Fix:

- Verify image name  
- Check registry credentials  
- Ensure network access  

---

#### e) Network / CNI Issues  

- Cluster networking misconfiguration can block scheduling (rare)

Fix:

- Check CNI plugin status  
- Verify cluster networking setup  

---

### 3. Quick Diagnostic Commands  

    kubectl get pods
    kubectl describe pod <nginx-pod-name>
    kubectl get nodes
    kubectl get events --sort-by=.metadata.creationTimestamp

---

### 4. Summary  

Pending means:

- Pod is created but **not scheduled yet**

Most common causes:

- Insufficient resources  
- NodeSelector / taints mismatch  
- PVC not bound  
- Image pull errors  

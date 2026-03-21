### Question  
How would you debug a failed deployment in Kubernetes?

---

### Answer  

### 1. Check Pod Status  

Start with:

    kubectl get pods

Look for states like:

- CrashLoopBackOff  
- Pending  
- Error  

For deeper details:

    kubectl describe pod <pod-name>

- Check **Events section** for root cause  

---

### 2. Examine Pod Logs  

    kubectl logs <pod-name>

For multi-container Pods:

    kubectl logs <pod-name> -c <container-name>

- Helps identify:
  - Application crashes  
  - Misconfigurations  
  - Dependency failures  

---

### 3. Inspect Deployment & ReplicaSet  

Check deployment:

    kubectl describe deployment <deployment-name>

- Look for:
  - Image issues  
  - Replica mismatch  
  - Failed rollouts  

Check ReplicaSets:

    kubectl get rs

- Ensure desired replicas are created  

---

### 4. Review Cluster Events  

    kubectl get events --sort-by=.metadata.creationTimestamp

- Look for:
  - FailedScheduling  
  - ImagePullBackOff  
  - Permission issues  

---

### 5. Check Resource Requests & Limits  

- Verify CPU / Memory configuration  

Example issue:

- Insufficient resources → Pod not scheduled  

Fix:

- Adjust requests/limits  
- Scale nodes if required  

---

### 6. Inspect Image & Registry Issues  

Common errors:

- ImagePullBackOff  
- ErrImagePull  

Check:

- Image name/tag  
- Registry credentials  

---

### 7. Check Networking & Services  

- Verify Service configuration  

    kubectl get svc

- Check endpoints:

    kubectl get endpoints <service-name>

- Inspect Network Policies if present  

---

### 8. Validate Configuration (ConfigMap / Secrets)  

- Missing or incorrect configs can crash pods  

Check:

    kubectl describe pod <pod-name>

- Look for mount or env errors  

---

### 9. Rollback Deployment (If Needed)  

    kubectl rollout undo deployment <deployment-name>

- Revert to last working version  

---

### 10. Check Node & Cluster Health  

    kubectl get nodes
    kubectl describe node <node-name>

- Look for:
  - Memory pressure  
  - Disk pressure  
  - Node not ready  

---

### 11. Advanced Debugging  

- Check metrics/logging tools:
  - Prometheus  
  - Grafana  
  - ELK stack  

- Use exec for live debugging:

    kubectl exec -it <pod-name> -- /bin/sh

---

### 12. Summary Approach  

| Step                  | What to Check                     |
|----------------------|----------------------------------|
| Pods                 | Status, events                   |
| Logs                 | Application errors               |
| Deployment           | Rollout issues                   |
| Events               | Scheduling / system failures     |
| Resources            | CPU / Memory limits              |
| Image                | Pull / registry issues           |
| Network              | Services / policies              |
| Config               | ConfigMap / Secrets              |
| Nodes                | Health / capacity                |

---

### 13. Key Insight  

- Always debug **layer by layer**:

    Deployment → ReplicaSet → Pod → Container → Application  

---

### Interview Summary  

To debug a failed Kubernetes deployment, follow a structured approach: check pod status and events, inspect logs, verify deployment and ReplicaSet behavior, review resource constraints and image issues, and validate networking and configuration. If needed, roll back to a stable version while investigating further.

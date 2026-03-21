### Question  
You're troubleshooting a Kubernetes pod that's failing to start. Walk me through your debugging process.

---

### Answer  

### 1. Check Pod Status  

    kubectl get pods <pod-name> -n <namespace>

Look at STATUS:

- Pending → Scheduling issue  
- CrashLoopBackOff → App keeps crashing  
- ImagePullBackOff / ErrImagePull → Image issues  
- Unknown → Node issue  

---

### 2. Describe the Pod  

    kubectl describe pod <pod-name> -n <namespace>

Focus on:

- Events (MOST IMPORTANT)  
- Node assignment  
- Container state (Waiting / Terminated reasons)  

---

### 3. Check Container Logs  

    kubectl logs <pod-name> -n <namespace>

Multi-container:

    kubectl logs <pod-name> -c <container-name> -n <namespace>

Previous crash:

    kubectl logs <pod-name> -c <container-name> --previous

---

### 4. Check Node Health  

    kubectl get nodes
    kubectl describe node <node-name>

Look for:

- Memory pressure  
- Disk pressure  
- Node taints  
- NotReady state  

---

### 5. Verify Image & Registry  

If image errors:

- Check image name/tag  
- Verify credentials  

Test manually:

    docker pull <image>:<tag>

---

### 6. Check Resource Requests & Limits  

- Insufficient resources → Pending  

Check in YAML:

    resources:
      requests:
      limits:

---

### 7. Validate ConfigMaps / Secrets / Volumes  

Common errors:

- CreateContainerConfigError  
- MountVolume failure  

Check:

- Config exists  
- Correct references  
- Permissions  

---

### 8. Debug Inside Container  

If container starts partially:

    kubectl exec -it <pod-name> -- /bin/sh

Also check init containers:

    kubectl logs <pod-name> -c <init-container-name>

---

### 9. Check Cluster Events  

    kubectl get events --sort-by=.metadata.creationTimestamp

- Helps identify system-level issues  

---

### 10. Apply Fix & Redeploy  

    kubectl apply -f pod.yaml
    kubectl get pods -w

---

### 11. Quick Debug Checklist  

| Symptom                         | Likely Cause                    | Action                         |
|--------------------------------|--------------------------------|--------------------------------|
| Pending                        | Scheduling/resource issue       | Check describe pod              |
| CrashLoopBackOff               | App crash                      | Check logs                     |
| ImagePullBackOff / ErrImagePull| Image / auth issue             | Verify image & secrets         |
| CreateContainerConfigError     | Config issue                   | Check ConfigMap/Secrets        |
| Node issues                    | Node unhealthy                 | Check node status              |

---

### 12. Key Insight  

- Always debug in layers:

    Pod → Container → Node → Cluster  

---

### Interview Summary  

To debug a failing pod, start by checking its status and describing it to inspect events. Then analyze logs, verify image and configuration, check node health and resources, and inspect volumes or secrets. Use interactive debugging if needed, and follow a layered approach to systematically identify and fix the issue.

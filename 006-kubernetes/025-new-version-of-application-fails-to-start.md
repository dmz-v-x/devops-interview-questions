### Question  
You deployed a new version of your application, but it fails to start, causing downtime for your users. How can you fix the problem?

---

### Answer  

### 1. Identify the Problem Quickly  

Check deployment and pods:

    kubectl get deployments -n <namespace>
    kubectl describe deployment <deployment-name> -n <namespace>
    kubectl get pods -n <namespace>

Look for:

- CrashLoopBackOff  
- ImagePullBackOff  
- FailedScheduling  
- Probe failures  

Check logs:

    kubectl logs <pod-name> -n <namespace>

---

### 2. Roll Back to a Stable Version (Immediate Fix)  

Restore service quickly:

    kubectl rollout undo deployment <deployment-name> -n <namespace>

Verify:

    kubectl rollout status deployment <deployment-name> -n <namespace>
    kubectl get pods -n <namespace>

- Ensures users are no longer impacted  

---

### 3. Debug the Failed Version  

---

#### Common Causes  

- Wrong image/tag  
- ConfigMap / Secret errors  
- Resource limits too low  
- Liveness / readiness probe failures  
- Dependency failures (DB, APIs)  

---

#### Debug Commands  

    kubectl describe pod <pod-name>
    kubectl logs <pod-name>

Optional:

- Temporarily increase resources  
- Disable probes to isolate issue  

---

### 4. Fix and Redeploy Safely  

- Update deployment YAML  

Apply:

    kubectl apply -f deployment.yaml

Monitor rollout:

    kubectl rollout status deployment <deployment-name>

Ensure:

- Readiness probes configured  
- Pods become ready before traffic  

---

### 5. Prevent Future Downtime  

---

#### Rolling Updates  

- Use:

  - maxUnavailable  
  - maxSurge  

---

#### Canary Deployment  

- Release to small % of users first  

---

#### Blue-Green Deployment  

- Switch traffic after validation  

---

#### Health Probes  

- readinessProbe → traffic control  
- livenessProbe → auto recovery  

---

#### Resource Configuration  

- Set proper CPU/memory requests & limits  

---

#### Auto Rollback  

- Use:

    progressDeadlineSeconds

- Automatically rollback failed deployments  

---

### 6. Summary  

| Step            | Action                                  |
|-----------------|------------------------------------------|
| Detect          | Check pods, logs, events                 |
| Recover         | Rollback to stable version               |
| Debug           | Identify root cause                      |
| Fix             | Update config/image                      |
| Redeploy        | Safe rollout                             |
| Prevent         | Use probes, canary, rollback strategies  |

---

### 7. Key Insight  

- First priority = **restore service (rollback)**  
- Second = **fix root cause**  

---

### Interview Summary  

When a deployment fails and causes downtime, immediately roll back to a stable version using `kubectl rollout undo` to restore service. Then debug the issue by checking logs, events, and configurations. After fixing the root cause, redeploy using safe rollout strategies like rolling updates, and implement safeguards such as readiness probes, canary deployments, and automatic rollback to prevent future failures.

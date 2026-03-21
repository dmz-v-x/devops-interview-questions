### Question  
How do you rollback a Kubernetes deployment?

---

### Answer  

### 1. Check Deployment History  

- Kubernetes keeps revision history of deployments  

Command:

    kubectl rollout history deployment <deployment-name>

---

### 2. Rollback to Previous Version  

- Revert to last working version  

Command:

    kubectl rollout undo deployment <deployment-name>

---

### 3. Rollback to Specific Revision  

- Choose a specific version  

Command:

    kubectl rollout undo deployment <deployment-name> --to-revision=<revision-number>

---

### 4. Verify Rollback  

- Ensure deployment is stable  

Command:

    kubectl rollout status deployment <deployment-name>

---

### 5. Monitor Pods  

    kubectl get pods -w

- Confirm old stable pods are running  

---

### 6. When to Use Rollback  

- New version crashes  
- High error rates  
- Performance issues  
- Misconfiguration  

---

### 7. Best Practices  

- Always use:

  - Rolling updates  
  - Readiness probes  

- Keep revision history enabled  
- Test in staging before production  

---

### 8. Summary  

| Step        | Command                                      |
|-------------|----------------------------------------------|
| History     | `kubectl rollout history deployment`         |
| Undo        | `kubectl rollout undo deployment`            |
| Specific    | `--to-revision=<n>`                          |
| Verify      | `kubectl rollout status deployment`          |

---

### 9. Key Insight  

- Rollback = **quick recovery mechanism**  
- Enables **zero/minimal downtime recovery**  

---

### Interview Summary  

Kubernetes provides built-in rollback functionality through the rollout command. You can view deployment history, revert to the previous version, or roll back to a specific revision. This allows quick recovery from failed deployments with minimal downtime, ensuring application stability.

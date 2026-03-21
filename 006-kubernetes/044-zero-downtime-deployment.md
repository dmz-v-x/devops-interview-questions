### Question  
How do you perform zero-downtime deployments in Kubernetes?

---

### Answer  

### 1. Use RollingUpdate Strategy  

- Default strategy in Kubernetes Deployments  

Example:

    strategy:
      type: RollingUpdate
      rollingUpdate:
        maxUnavailable: 0
        maxSurge: 1

---

#### Explanation  

- maxUnavailable: 0  
  → No downtime, all existing pods stay available  

- maxSurge: 1  
  → Add 1 extra pod during update  

---

### 2. Configure Readiness Probes  

- Ensures pod is **ready before receiving traffic**  

Example:

    readinessProbe:
      httpGet:
        path: /health
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5

---

### 3. Use Liveness Probes  

- Detects unhealthy pods  
- Automatically restarts them  

---

### 4. Use Service Abstraction  

- Services route traffic only to **healthy pods**  

- During rollout:

  - New pods added to service  
  - Old pods removed gradually  

---

### 5. Ensure Sufficient Replicas  

- Maintain multiple replicas  

Example:

    replicas: 3

- Guarantees availability during updates  

---

### 6. Monitor Deployment  

    kubectl rollout status deployment <deployment-name>

Watch pods:

    kubectl get pods -w

---

### 7. Rollback if Needed  

    kubectl rollout undo deployment <deployment-name>

---

### 8. Advanced Strategies  

---

#### Canary Deployment  

- Release to small % of users  
- Gradually increase traffic  

---

#### Blue-Green Deployment  

- Two environments:

  - Blue → current  
  - Green → new  

- Switch traffic instantly  

---

### 9. Summary  

| Technique            | Purpose                              |
|----------------------|--------------------------------------|
| RollingUpdate        | Gradual replacement                  |
| Readiness Probe      | Ensure pods are ready                |
| Liveness Probe       | Restart unhealthy pods               |
| Service              | Load balance traffic                 |
| Replicas             | Maintain availability                |
| Canary / Blue-Green  | Safer advanced rollouts              |

---

### 10. Key Insight  

- Zero downtime = **never route traffic to unready pods**  
- Controlled rollout ensures continuous availability  

---

### Interview Summary  

Zero-downtime deployments in Kubernetes are achieved using rolling updates with proper configuration of maxUnavailable and maxSurge, combined with readiness probes to ensure only healthy pods receive traffic. Services handle load balancing across pods, while advanced strategies like canary and blue-green deployments provide additional safety during upgrades.

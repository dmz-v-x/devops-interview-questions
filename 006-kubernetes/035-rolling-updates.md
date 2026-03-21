### Question  
Your team wants to implement rolling updates for a Kubernetes deployment to minimize downtime during application upgrades. How would you achieve this?

---

### Answer  

### 1. Use Deployment with RollingUpdate Strategy  

- Kubernetes Deployments support rolling updates by default  

Example:

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: myapp
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxUnavailable: 1
          maxSurge: 1
      template:
        metadata:
          labels:
            app: myapp
        spec:
          containers:
          - name: web
            image: myapp:v1
            ports:
            - containerPort: 80

---

### 2. Understand Key Parameters  

- maxUnavailable: 1  
  → Only 1 pod can go down during update  

- maxSurge: 1  
  → Allows 1 extra pod during rollout  

Result:

- At least **2 pods always serving traffic**  

---

### 3. Trigger Rolling Update  

Update image:

    kubectl set image deployment/myapp web=myapp:v2

Kubernetes will:

- Create new pods (v2)  
- Gradually terminate old pods (v1)  

---

### 4. Monitor Rollout  

    kubectl rollout status deployment/myapp

Watch pods:

    kubectl get pods -w

---

### 5. Rollback if Needed  

    kubectl rollout undo deployment/myapp

- Quickly revert to previous stable version  

---

### 6. Ensure Zero Downtime  

---

#### Use Readiness Probes  

- Only route traffic to ready pods  

---

#### Use Liveness Probes  

- Restart unhealthy pods  

---

#### Use Proper Replica Count  

- Always keep multiple replicas  

---

### 7. Advanced Enhancements  

- Combine with HPA for scaling  
- Use PodDisruptionBudgets to maintain minimum availability  
- Add canary deployment for safer rollout  

---

### 8. Summary  

| Step            | Action                                  |
|-----------------|------------------------------------------|
| Configure       | RollingUpdate strategy                   |
| Update          | Change image version                     |
| Monitor         | Track rollout                            |
| Rollback        | Undo if failure                          |
| Optimize        | Probes + scaling                         |

---

### 9. Key Insight  

- Rolling updates = **gradual replacement without downtime**  
- Controlled via **maxSurge + maxUnavailable**  

---

### Interview Summary  

To implement rolling updates, configure a Deployment with a RollingUpdate strategy using maxUnavailable and maxSurge to control availability. Update the container image to trigger the rollout, monitor progress, and use readiness probes to ensure traffic is only sent to healthy pods. This ensures minimal or zero downtime during application upgrades.

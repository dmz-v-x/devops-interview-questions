### Question  
How do you implement zero-downtime deployments in Kubernetes?

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
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxSurge: 1
          maxUnavailable: 0
      selector:
        matchLabels:
          app: myapp
      template:
        metadata:
          labels:
            app: myapp
        spec:
          containers:
          - name: myapp
            image: myapp:v2

---

#### Key Fields  

| Field            | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| maxSurge         | Extra pods created during update                                            |
| maxUnavailable   | Pods allowed to be down (0 = zero downtime)                                 |

---

### 2. Configure Readiness Probes  

- Ensures pods receive traffic **only when ready**  

Example:

    readinessProbe:
      httpGet:
        path: /health
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10

---

### 3. Use Liveness Probes  

- Detects unhealthy pods  
- Restarts automatically  

Example:

    livenessProbe:
      httpGet:
        path: /health
        port: 8080
      initialDelaySeconds: 10
      periodSeconds: 10

---

### 4. Use Service for Load Balancing  

- Service routes traffic only to **healthy pods**  

- During update:

  - New pods added  
  - Old pods removed gradually  

---

### 5. Ensure Multiple Replicas  

- Maintain availability  

Example:

    replicas: 3

---

### 6. Monitor Rollout  

    kubectl rollout status deployment myapp
    kubectl get pods -w

---

### 7. Rollback if Needed  

    kubectl rollout undo deployment myapp

---

### 8. Advanced Strategies  

---

#### Blue-Green Deployment  

- Two environments  
- Switch traffic instantly  

---

#### Canary Deployment  

- Gradual rollout  
- Monitor before full release  

---

### 9. Summary  

| Technique        | Purpose                              |
|------------------|--------------------------------------|
| RollingUpdate    | Gradual replacement                  |
| Readiness Probe  | Ensure pod readiness                 |
| Liveness Probe   | Restart unhealthy pods               |
| Service          | Traffic routing                      |
| Replicas         | Maintain availability                |
| Canary/BlueGreen | Safer advanced rollout               |

---

### 10. Key Insight  

- Zero downtime = **no traffic to unready pods**  
- Controlled rollout ensures continuous service  

---

### Interview Summary  

Zero-downtime deployments in Kubernetes are achieved using rolling updates with maxUnavailable set to 0 and maxSurge configured appropriately. Readiness probes ensure traffic is only routed to healthy pods, while Services handle load balancing. Additional strategies like canary or blue-green deployments further enhance deployment safety and reliability.

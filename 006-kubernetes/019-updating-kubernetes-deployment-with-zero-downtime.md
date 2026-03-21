### Question  
You're tasked with updating a Kubernetes deployment without downtime. How would you achieve zero-downtime deployments?

---

### Answer  

### 1. Use Deployment with RollingUpdate Strategy  

- Kubernetes Deployments support **rolling updates by default**  

Example:

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-app
    spec:
      replicas: 3
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxUnavailable: 1
          maxSurge: 1
      selector:
        matchLabels:
          app: my-app
      template:
        metadata:
          labels:
            app: my-app
        spec:
          containers:
            - name: app
              image: my-app:v2
              ports:
                - containerPort: 80

Explanation:

- maxUnavailable → ensures minimum pods always running  
- maxSurge → allows extra pods during update  

---

### 2. Configure Readiness Probes  

- Prevent traffic to unready pods  

Example:

    readinessProbe:
      httpGet:
        path: /health
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5

- Pod receives traffic **only after passing readiness check**  

---

### 3. Configure Liveness Probes  

- Restart unhealthy containers automatically  

Example:

    livenessProbe:
      httpGet:
        path: /health
        port: 80
      initialDelaySeconds: 15
      periodSeconds: 20

- Maintains application stability  

---

### 4. Use Kubernetes Service for Load Balancing  

- Service routes traffic only to **ready pods**  

- Ensures:
  - No downtime  
  - Continuous availability  

---

### 5. Advanced Deployment Strategies  

---

#### A. Canary Deployment  

- Release to small subset first  

Steps:

- Deploy new version with fewer replicas  
- Monitor performance  
- Gradually increase rollout  

---

#### B. Blue-Green Deployment  

- Two environments:

  - Blue → current  
  - Green → new  

- Switch traffic after validation  

- Requires Ingress or external load balancer  

---

### 6. Monitor Rollout  

    kubectl rollout status deployment my-app
    kubectl get pods -w
    kubectl describe pod <pod-name>

---

### 7. Rollback if Needed  

    kubectl rollout undo deployment my-app

- Instantly revert to previous stable version  

---

### 8. Summary  

| Technique                | Purpose                                      |
|--------------------------|----------------------------------------------|
| RollingUpdate            | Gradual updates without downtime             |
| Readiness Probe          | Ensure only ready pods receive traffic       |
| Liveness Probe           | Maintain pod health                          |
| Service Load Balancing   | Distribute traffic safely                    |
| Canary / Blue-Green      | Safe progressive rollout                     |
| Monitoring & Rollback    | Detect and recover from failures             |

---

### 9. Key Insight  

- Zero downtime = **Never drop below minimum healthy pods**  

---

### Interview Summary  

Zero-downtime deployments in Kubernetes are achieved using rolling updates with proper configuration of maxUnavailable and maxSurge, combined with readiness probes to ensure traffic is only sent to healthy pods. Advanced strategies like canary or blue-green deployments further enhance safety, while monitoring and rollback mechanisms ensure reliability during updates.

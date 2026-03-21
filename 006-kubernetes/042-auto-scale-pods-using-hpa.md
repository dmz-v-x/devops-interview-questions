### Question  
How do you auto-scale pods in Kubernetes using HPA?

---

### Answer  

### 1. What is HPA  

- **Horizontal Pod Autoscaler (HPA)** automatically adjusts the number of pods  

- Based on:

  - CPU  
  - Memory  
  - Custom metrics  

---

### 2. Prerequisite: Metrics Server  

- Required to collect resource usage  

Install:

    kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

Verify:

    kubectl top pods

---

### 3. Define Deployment with Resources  

- HPA works based on **resource requests**

Example:

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx
            resources:
              requests:
                cpu: "100m"
              limits:
                cpu: "500m"

---

### 4. Create HPA  

---

#### Using Command  

    kubectl autoscale deployment nginx-deployment \
      --cpu-percent=50 \
      --min=1 \
      --max=10

---

#### Using YAML  

    apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: nginx-hpa
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: nginx-deployment
      minReplicas: 1
      maxReplicas: 10
      metrics:
      - type: Resource
        resource:
          name: cpu
          target:
            type: Utilization
            averageUtilization: 50

---

### 5. How HPA Works  

- Monitors average CPU across pods  

If:

- CPU > 50% → scale up  
- CPU < 50% → scale down  

Within limits:

- Min: 1  
- Max: 10  

---

### 6. Check Status  

    kubectl get hpa

Detailed view:

    kubectl describe hpa nginx-hpa

---

### 7. Important Notes  

- Must define **resource requests**  
- Works best with **stateless apps**  
- Combine with:

  - Cluster Autoscaler  
  - Readiness probes  

---

### 8. Summary  

| Step            | Action                          |
|-----------------|----------------------------------|
| Install         | Metrics Server                   |
| Configure       | Deployment with resources        |
| Create          | HPA (CPU-based)                  |
| Monitor         | `kubectl get hpa`               |
| Scale           | Auto based on usage              |

---

### 9. Key Insight  

- HPA = **automatic horizontal scaling based on load**  

---

### Interview Summary  

To auto-scale pods in Kubernetes, use the Horizontal Pod Autoscaler (HPA). It monitors metrics like CPU utilization and dynamically adjusts the number of pod replicas within defined limits. This ensures applications can handle varying load efficiently while optimizing resource usage.

### Question  
How do you implement auto-healing in Kubernetes? Also, how do you auto-scale pods using HPA with custom metrics?

---

### Answer  

### 1. What is Auto-Healing  

- Kubernetes automatically detects and fixes failures  

Ensures:

- Desired state is always maintained  

---

### 2. Liveness & Readiness Probes  

---

#### Liveness Probe  

- Detects if container is unhealthy  
- Restarts container if it fails  

Example:

    livenessProbe:
      httpGet:
        path: /health
        port: 80
      initialDelaySeconds: 10
      periodSeconds: 5

---

#### Readiness Probe  

- Checks if pod is ready to serve traffic  
- Removes pod from Service if not ready  

Example:

    readinessProbe:
      httpGet:
        path: /ready
        port: 80

---

### 3. ReplicaSet / Deployment  

- Ensures desired number of pods  

If:

- Pod crashes → new pod created  
- Pod deleted → recreated automatically  

---

### 4. Node Auto-Healing  

- Failed nodes → pods rescheduled  

With:

- Cluster Autoscaler  
- Cloud provider integration  

---

### 5. Self-Healing Flow  

- Container fails → liveness probe fails  
- Kubernetes restarts container  
- If pod dies → ReplicaSet creates new one  
- If node fails → pods rescheduled  

---

### 6. Custom Metrics Autoscaling (HPA)  

---

### Step 1: Install Metrics Adapter  

- Required to use custom metrics  

Example:

    helm install prometheus-adapter prometheus-community/prometheus-adapter \
      --namespace monitoring

---

### Step 2: Expose Custom Metric  

Example metric:

- http_requests_per_second  

---

### Step 3: Create HPA with Custom Metrics  

    apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: custom-hpa
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: my-app
      minReplicas: 2
      maxReplicas: 15
      metrics:
      - type: Pods
        pods:
          metric:
            name: http_requests_per_second
          target:
            type: AverageValue
            averageValue: "100"

---

### 7. How Custom HPA Works  

- Monitors metric (e.g., RPS per pod)  

If:

- > 100 RPS → scale up  
- < threshold → scale down  

---

### 8. Check HPA  

    kubectl get hpa
    kubectl describe hpa custom-hpa

---

### 9. Best Practices  

- Combine:

  - CPU-based scaling  
  - Custom metrics  

- Ensure:

  - Prometheus + Adapter highly available  

- Avoid rapid scaling:

  - Use cooldown / stabilization windows  

---

### 10. Summary  

| Feature            | Purpose                                |
|--------------------|----------------------------------------|
| Liveness Probe     | Restart unhealthy containers           |
| Readiness Probe    | Control traffic routing                |
| ReplicaSet         | Maintain pod count                     |
| Node Recovery      | Reschedule pods                        |
| HPA (custom)       | Scale based on app metrics             |

---

### 11. Key Insight  

- Auto-healing = **detect + recover automatically**  
- Custom HPA = **scale based on real business metrics**  

---

### Interview Summary  

Kubernetes implements auto-healing using liveness and readiness probes, ReplicaSets, and node recovery mechanisms to automatically restart or replace failed components. For advanced scaling, HPA can use custom metrics like request rate via Prometheus adapters, enabling scaling decisions based on real application load rather than just CPU or memory.

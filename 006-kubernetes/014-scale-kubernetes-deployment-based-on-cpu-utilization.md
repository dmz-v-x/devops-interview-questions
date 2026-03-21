### Question  
You need to scale a Kubernetes deployment based on CPU utilization. Describe how you would implement autoscaling.

---

### Answer  

### 1. Overview  

- Use **Horizontal Pod Autoscaler (HPA)**  
- Automatically scales Pods based on CPU usage  

---

### 2. Ensure Metrics Server is Installed  

HPA depends on metrics data.

Install:

    kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.5.0/components.yaml

Verify:

    kubectl top pods

---

### 3. Define CPU Requests & Limits  

Required for HPA to calculate utilization.

Example:

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-deployment
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: my-app
      template:
        metadata:
          labels:
            app: my-app
        spec:
          containers:
            - name: my-container
              image: my-app-image
              resources:
                requests:
                  cpu: "100m"
                limits:
                  cpu: "500m"

---

### 4. Create Horizontal Pod Autoscaler (HPA)  

---

#### Option 1: Using Command  

    kubectl autoscale deployment my-deployment --cpu-percent=50 --min=2 --max=10

---

#### Option 2: Using YAML  

    apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: my-deployment-hpa
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: my-deployment
      minReplicas: 2
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

- Monitors CPU usage via Metrics Server  
- Compares with target (e.g., 50%)  

Behavior:

- CPU > target → scale up  
- CPU < target → scale down  

---

### 6. Monitor Autoscaling  

    kubectl get hpa

Shows:

- Current CPU usage  
- Desired replicas  
- Current replicas  

---

### 7. Fine-Tuning  

- Adjust:

  - minReplicas  
  - maxReplicas  
  - target CPU  

- Use custom metrics if needed  

---

### 8. Best Practices  

- Always define resource requests  
- Avoid too low/high CPU targets  
- Combine with:

  - Pod anti-affinity  
  - Cluster autoscaler (node scaling)  

---

### 9. Summary  

| Step                 | Action                                  |
|----------------------|------------------------------------------|
| Metrics Server       | Enable resource metrics                  |
| Resource Requests    | Define CPU usage baseline                |
| HPA                  | Configure autoscaling rules              |
| Monitoring           | Track scaling behavior                   |
| Fine-Tuning          | Adjust thresholds                        |

---

### 10. Key Insight  

- HPA scales **Pods**, not nodes  
- Works based on **relative CPU utilization (%)**  

---

### Interview Summary  

To implement autoscaling based on CPU utilization, install the Metrics Server, define CPU requests/limits in the deployment, and configure a Horizontal Pod Autoscaler (HPA) with a target CPU percentage. HPA continuously monitors usage and automatically scales the number of pods up or down to maintain the desired performance.

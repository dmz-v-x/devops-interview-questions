### Question  
Previously created Nginx web server deployed successfully, but the web page is not accessible. Find out why?

---

### Answer  

### 1. Check Pod Status  

Start with:

    kubectl get pods

- Pod should be in **Running** state  

If not, check logs:

    kubectl logs <nginx-pod-name>

---

### 2. Check if Pod is Listening on Correct Port  

Nginx usually listens on **port 80**.

    kubectl exec -it <nginx-pod-name> -- netstat -tuln

Verify that port **80 is open** inside the container.

---

### 3. Check Service  

Pods are typically exposed via a **Service**.

    kubectl get svc

Ensure:

- Service exists  
- Correct type (NodePort / LoadBalancer)  
- Selector matches Pod labels  

Example:

    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-service
    spec:
      selector:
        app: nginx
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
      type: NodePort

---

### 4. Common Reasons for Inaccessibility  

---

#### a) No Service or Wrong Selector  

Service selector must match Pod labels.

Check labels:

    kubectl get pod <nginx-pod-name> --show-labels

Fix:

- Update Service selector OR Pod labels  

---

#### b) Wrong Service Type  

- ClusterIP → internal only  
- NodePort → external via node IP  
- LoadBalancer → external (cloud only)  

Fix:

- Use NodePort or LoadBalancer for external access  

---

#### c) Firewall / Network Restrictions  

- NodePort may be blocked  

Fix:

- Open required ports in firewall  
- Use correct node IP and NodePort  

---

#### d) Readiness Probe Failure  

If readiness probe fails → traffic not routed.

Check:

    kubectl describe pod <nginx-pod-name>

Fix:

- Correct readiness probe configuration  

---

#### e) Incorrect Port Mapping  

Service targetPort must match container port (80 for Nginx).

Fix:

- Ensure:

        targetPort: 80

---

### 5. Quick Troubleshooting Commands  

    kubectl describe pod <nginx-pod-name>
    kubectl get svc nginx-service -o wide
    kubectl get endpoints nginx-service
    kubectl exec -it <nginx-pod-name> -- curl localhost

---

### 6. Key Debug Insight  

- If `curl localhost` inside Pod works → Nginx is fine  
- If Service endpoints are empty → Service is not linked to Pod  

---

### 7. Summary  

| Cause                     | How to check/fix                                                |
|--------------------------|-----------------------------------------------------------------|
| Service selector mismatch| Ensure labels match (`kubectl get pod --show-labels`)           |
| Service type wrong       | Use NodePort / LoadBalancer                                     |
| Firewall issues          | Open NodePort range                                             |
| Readiness probe failing  | Check `kubectl describe pod`                                    |
| Port mismatch            | Ensure `targetPort` = container port (80)                       |

### Question  
You are getting a 502 Bad Gateway in a Kubernetes Ingress. How do you troubleshoot?

---

### Answer  

### 1. Understand the Problem  

- 502 = Ingress **cannot reach backend service**  

---

### 2. Check Ingress Controller Logs  

    kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --tail=100

Look for:

- connection refused  
- timeout  
- upstream errors  

---

### 3. Verify Ingress Configuration  

    kubectl get ingress <ingress-name> -o yaml

Check:

- Correct service name  
- Correct port  
- Path routing  

---

### 4. Check Service  

    kubectl get svc <service-name> -o yaml

Verify:

- Port matches container  
- Selector matches pods  

---

#### Check Endpoints  

    kubectl get endpoints <service-name>

- If empty → Service not linked to pods  

---

### 5. Check Backend Pods  

    kubectl get pods -l app=<label>

- Ensure pods are **Running**  

Check logs:

    kubectl logs <pod-name>

- Look for app crashes  

---

### 6. Check Network Policies  

    kubectl get networkpolicy

- Ensure traffic allowed:

  - Ingress → Service  
  - Pod ↔ Pod  

---

### 7. Check DNS Resolution  

    kubectl run -it --rm debug --image=busybox --restart=Never -- nslookup <service-name>

- Ensure service resolves correctly  

---

### 8. Check Resource Usage  

    kubectl top pod <pod-name>

- High CPU/memory → app may fail  

---

### 9. Check Ingress Annotations  

Example (NGINX):

    nginx.ingress.kubernetes.io/proxy-read-timeout: "300"

- Misconfigured timeouts → 502 errors  

---

### 10. Check Load Balancer / External Setup  

- Verify cloud LB is routing correctly  
- Ensure health checks pass  

---

### 11. Check SSL/TLS Configuration  

- Validate certificates  
- Ensure correct secret is used  

---

### 12. Summary  

| Area              | What to Check                        |
|-------------------|-------------------------------------|
| Ingress           | Config, paths, backend              |
| Service           | Ports, selectors, endpoints         |
| Pods              | Status, logs                        |
| Network           | Policies, DNS                       |
| Infra             | LB, TLS                             |

---

### 13. Key Insight  

- 502 usually means:
  - Service not reachable  
  - No endpoints  
  - App crash  

---

### Interview Summary  

A 502 Bad Gateway in Kubernetes Ingress typically indicates that the Ingress controller cannot communicate with the backend service. Troubleshooting involves checking Ingress configuration, service endpoints, pod health, network policies, DNS resolution, and load balancer or TLS settings. The root cause is usually a misconfigured service, missing endpoints, or unhealthy backend pods. 

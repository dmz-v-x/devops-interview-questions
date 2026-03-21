### Question  
You deployed an Nginx web server in Kubernetes, and the Pod is running fine, but the application is not accessible via the exposed URL. What can you do about it?

---

### Answer  

### 1. Verify Pod is Running Correctly  

    kubectl get pods -n <namespace>
    kubectl describe pod <nginx-pod> -n <namespace>
    kubectl logs <nginx-pod> -n <namespace>

Check:

- STATUS = Running  
- No errors in logs  
- Container listening on port 80  

---

### 2. Check the Service  

    kubectl get svc -n <namespace>
    kubectl describe svc <service-name> -n <namespace>

Verify:

- Correct **Service type** (ClusterIP / NodePort / LoadBalancer)  
- Port mapping:

        port: 80
        targetPort: 80

---

#### Validate Selector (VERY COMMON ISSUE)  

    kubectl get pods --show-labels -n <namespace>
    kubectl get svc -o yaml -n <namespace>

- Service selector must match Pod labels  

---

### 3. Test Internal Connectivity  

Run a temporary pod:

    kubectl run curlpod --image=curlimages/curl -it --rm -- /bin/sh

Test:

    curl http://<service-name>:<port>

Result:

- Works → issue is external  
- Fails → issue is Service or Pod  

---

### 4. Verify External Access  

---

#### A. NodePort  

    kubectl get svc <service-name> -o wide -n <namespace>

- Access:

    http://<Node-IP>:<NodePort>

Check:

- Firewall rules  
- Correct Node IP  

---

#### B. LoadBalancer  

- Ensure EXTERNAL-IP is assigned  

    kubectl get svc

Check:

- Cloud provider status  
- Security groups  

---

#### C. Ingress  

    kubectl get ingress -n <namespace>
    kubectl describe ingress <ingress-name> -n <namespace>

Verify:

- Hostname  
- Path routing  
- Backend service mapping  

Also ensure:

- Ingress controller is running  

---

### 5. Check Network Policies  

    kubectl get networkpolicy -n <namespace>

- Ensure traffic is allowed from:
  - External clients  
  - Ingress controller  

---

### 6. Check DNS / URL  

- Ensure domain resolves correctly  

    nslookup <your-domain>

---

### 7. Summary  

| Area                  | Check                                  |
|-----------------------|----------------------------------------|
| Pod                   | Running, logs OK                       |
| Service               | Ports + selector match                 |
| Internal access       | curl inside cluster                    |
| External exposure     | NodePort / LB / Ingress config         |
| Network policies      | Allow traffic                          |
| DNS                   | Correct IP resolution                  |

---

### 8. Common Causes  

- Service selector mismatch  
- Wrong port / targetPort  
- Ingress misconfiguration  
- Firewall blocking traffic  
- NetworkPolicy restrictions  

---

### 9. Key Insight  

- Always debug step-by-step:

    Pod → Service → Internal → External  

---

### Interview Summary  

If a running Nginx pod is not accessible, verify pod health, check service configuration and selector labels, test internal connectivity, and then validate external exposure via NodePort, LoadBalancer, or Ingress. Most issues arise from selector mismatches, port misconfigurations, or networking restrictions.

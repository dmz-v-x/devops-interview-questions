### Question  
How can you secure a Kubernetes cluster?

---

### Answer  

### 1. Cluster Access & Authentication  

---

#### Enable RBAC  

- Apply **least privilege principle**  

Example:

    kubectl create rolebinding developer-binding --clusterrole=view --user=developer

---

#### Secure Authentication  

- Use:

  - OIDC  
  - LDAP  
  - Cloud IAM  

- Avoid static tokens  

---

### 2. Network Security  

---

#### Network Policies  

- Control pod-to-pod communication  

Example:

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-backend
      namespace: default
    spec:
      podSelector:
        matchLabels:
          app: backend
      policyTypes:
        - Ingress
      ingress:
        - from:
            - podSelector:
                matchLabels:
                  app: frontend

---

#### Secure Ingress  

- Use HTTPS (TLS)  
- Restrict access via firewall/security groups  

---

### 3. Secrets Management  

- Use Kubernetes Secrets  

- Avoid hardcoding credentials  

- Use external tools:

  - Vault  
  - AWS Secrets Manager  
  - Azure Key Vault  

---

#### Encrypt Secrets at Rest  

- Enable encryption in etcd  

---

### 4. Pod & Workload Security  

---

#### Pod Security Standards  

- Avoid root user  
- Drop unnecessary capabilities  
- Use read-only filesystem  

---

#### Resource Limits  

    resources:
      requests:
        cpu: "100m"
        memory: "128Mi"
      limits:
        cpu: "500m"
        memory: "512Mi"

---

#### Security Context  

    securityContext:
      runAsUser: 1000
      runAsGroup: 3000
      fsGroup: 2000

---

### 5. Cluster Component Security  

- Keep cluster updated  
- Secure API server:

  - Disable anonymous access  
  - Enable audit logs  
  - Restrict IP access  

---

#### Secure etcd  

- Enable encryption  
- Use TLS communication  

---

### 6. Image & Supply Chain Security  

- Use trusted images  
- Scan for vulnerabilities (Trivy, etc.)  
- Use signed images  
- Restrict registries  

---

### 7. Monitoring & Auditing  

---

#### Audit Logs  

- Track all API activity  

---

#### Monitoring  

- Prometheus + Grafana  

---

#### Alerting  

- Detect anomalies (unexpected pods, spikes)  

---

### 8. Advanced Enhancements  

- Service Mesh → mTLS encryption  
- Pod Security Admission → enforce policies  
- Security tools:

  - Kube-bench  
  - Kube-hunter  
  - Trivy  

---

### 9. Summary  

| Area              | Security Measure                          |
|------------------|-------------------------------------------|
| Access           | RBAC + OIDC                              |
| Network          | Network Policies + TLS                   |
| Secrets          | Secrets + encryption                     |
| Workloads        | SecurityContext + limits                 |
| Components       | API server + etcd security               |
| Supply Chain     | Image scanning & signing                 |
| Monitoring       | Logs + alerts                            |

---

### 10. Key Insight  

- Security = **Layered approach (Defense in Depth)**  

---

### Interview Summary  

To secure a Kubernetes cluster, implement strong authentication and RBAC-based authorization, enforce network policies, protect secrets with encryption and external managers, secure workloads using security contexts and policies, harden cluster components, and ensure continuous monitoring and auditing. A layered security approach ensures comprehensive protection across the entire system.

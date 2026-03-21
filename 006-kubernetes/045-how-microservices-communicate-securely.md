### Question  
How do microservices communicate securely in Kubernetes?

---

### Answer  

### 1. Network Policies  

- Control **which pods can communicate**  

- Define allow/deny rules  

Example:

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-backend
    spec:
      podSelector:
        matchLabels:
          app: backend
      ingress:
        - from:
            - podSelector:
                matchLabels:
                  app: frontend

- Requires CNI like:

  - Calico  
  - Cilium  

---

### 2. Mutual TLS (mTLS) via Service Mesh  

- Encrypts **service-to-service traffic**  
- Verifies service identity  

Tools:

- Istio  
- Linkerd  
- Consul  

Benefits:

- Automatic certificate rotation  
- Encryption in transit  
- Authentication between services  

---

### 3. Role-Based Access Control (RBAC)  

- Restricts access to Kubernetes APIs  

- Apply **least privilege principle**  

Example:

- Limit which services can access secrets or resources  

---

### 4. Service Accounts & Secrets  

- Assign **dedicated service accounts** per service  

- Store sensitive data in:

  - Kubernetes Secrets  
  - Vault  

Example:

    env:
      - name: DB_PASSWORD
        valueFrom:
          secretKeyRef:
            name: db-secret
            key: password

---

### 5. Internal Cluster Communication  

- Use Kubernetes DNS:

    http://service-name.namespace.svc.cluster.local

- Keeps traffic **internal to cluster**  

---

### 6. Monitoring & Auditing  

- Track communication patterns  

Tools:

- Prometheus  
- Grafana  
- OpenTelemetry  
- Kiali  

- Detect:

  - Unauthorized access  
  - Anomalies  

---

### 7. Summary  

| Layer              | Security Measure                     |
|--------------------|--------------------------------------|
| Network            | Network Policies                    |
| Transport          | mTLS (Service Mesh)                 |
| Access Control     | RBAC                               |
| Identity           | Service Accounts                   |
| Secrets            | Secrets / Vault                    |
| Observability      | Monitoring & auditing              |

---

### 8. Key Insight  

- Security = **multiple layers (defense in depth)**  
- Combine **network + identity + encryption**  

---

### Interview Summary  

Microservices in Kubernetes communicate securely using a layered approach. Network policies restrict traffic between pods, while service meshes like Istio enable mutual TLS for encrypted and authenticated communication. RBAC and service accounts enforce least privilege access, and secrets are securely managed using Kubernetes Secrets or external tools like Vault. Internal DNS ensures traffic stays within the cluster, and monitoring tools help detect anomalies and enforce security policies.

### Question  
What are different types of Services in Kubernetes?

---

### Answer  

### 1. Overview  

A **Service** in Kubernetes provides a **stable way to access Pods**, even though Pods are ephemeral.

- Provides:
  - Stable IP  
  - Stable DNS name  

---

### 2. Types of Services  

---

#### 1. ClusterIP (Default)  

- Accessible **only داخل cluster**  

Spec:

    spec:
      type: ClusterIP

Use case:

- Internal communication (app ↔ DB, microservices)

Example:

- MySQL service used only by backend  

---

#### 2. NodePort  

- Exposes service on each node’s IP  

Access:

    <NodeIP>:<NodePort>

Spec:

    spec:
      type: NodePort

- Port range: **30000–32767**

Use case:

- Testing / simple external access  

---

#### 3. LoadBalancer  

- Creates **external load balancer** (cloud only)  

Spec:

    spec:
      type: LoadBalancer

Use case:

- Public-facing applications  

Example:

- Exposing frontend to internet  

---

#### 4. ExternalName  

- Maps service to **external DNS**  

Spec:

    spec:
      type: ExternalName
      externalName: mydb.example.com

- No Pods or selector  

Use case:

- Access external services (DB, APIs)  

---

#### 5. Headless Service  

- No cluster IP  

Spec:

    spec:
      clusterIP: None

- Returns **Pod IPs directly**  

Use case:

- Stateful apps  
- Direct pod communication  

---

### 3. Summary  

| Service Type | Scope                          | Use Case                         |
|--------------|--------------------------------|----------------------------------|
| ClusterIP    | Internal cluster only          | Microservices, DB access         |
| NodePort     | NodeIP:Port                   | Testing / simple external access |
| LoadBalancer | External LB (cloud)           | Public apps                      |
| ExternalName | DNS alias                     | External services                |
| Headless     | No ClusterIP, direct Pod DNS  | Stateful apps                    |

---

### 4. Key Insight  

- Service = **stable access layer over Pods**  
- Choose type based on **exposure level (internal vs external)**  

---

### Interview Summary  

Kubernetes provides multiple Service types to expose applications at different levels. ClusterIP is used for internal communication, NodePort and LoadBalancer expose services externally, ExternalName maps to external services, and Headless services enable direct pod-level communication for stateful workloads.

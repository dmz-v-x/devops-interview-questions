### Question  
What is the disadvantage of LoadBalancer service type in Kubernetes?

---

### Answer  

The main disadvantages of the LoadBalancer service type are:

- Cost overhead  
- Scalability limitations  
- Vendor lock-in  
- Lack of advanced routing capabilities  

---

### LoadBalancer: Quick Recap

When you define a service with type LoadBalancer, Kubernetes requests the cloud provider (AWS, Azure, GCP, etc.) to provision a cloud-native Layer 4 load balancer.

```yaml
spec:
  type: LoadBalancer
  ports:
    - port: 80
```

- The load balancer routes traffic to backend pods via cluster nodes  

---

### Key Disadvantages

---

### 1. Cost Overhead

- Each LoadBalancer service creates:
  - A separate cloud load balancer  

- Example:
  - In AWS → multiple ELBs  

- Problem:
  - Costs incurred even when idle  

- Scenario:
  - Multiple microservices → multiple LBs → unnecessary expense  

---

### 2. Scalability and Management

- One-to-one mapping:
  - One service = one load balancer  

- Issues:
  - Difficult to manage at scale  
  - Operational overhead increases  

---

### 3. Vendor Lock-In

- Depends on:
  - Cloud provider integration  

- Limitations:
  - Does not work natively on:
    - Bare metal  
    - Local environments  

- Requires:
  - External solutions (e.g., MetalLB)  

---

### 4. No Layer 7 (HTTP) Routing

- Supports only:
  - Layer 4 (TCP/UDP)  

- Limitations:
  - No path-based routing (/api, /web)  
  - No host-based routing  

---

### Alternative Approach

---

### Use Ingress Controller

- Examples:
  - NGINX Ingress  
  - AWS ALB Ingress  

---

### Benefits

- Single load balancer  
- Multiple services supported  
- Advanced routing:
  - Path-based  
  - Host-based  

- SSL termination  
- Cost optimization  

---

### Key Takeaways

- LoadBalancer:
  - Simple but limited  

- Ingress:
  - Scalable and flexible  

---

### Interview-Ready Summary

“The LoadBalancer service type creates a separate cloud load balancer for each service, which increases cost and makes management difficult at scale. It also causes vendor lock-in since it depends on cloud provider integrations and lacks advanced Layer 7 routing features like path-based routing. In practice, I prefer using an Ingress controller, which allows a single load balancer to route traffic to multiple services, providing better flexibility and cost efficiency.”

### Question  
What is a Namespace in Kubernetes?

---

### Answer  

### 1. Definition  

A **Namespace** in Kubernetes is a way to **logically divide a cluster into virtual clusters**.

- Helps organize and isolate resources  
- Used for multi-team or multi-environment setups  

---

### 2. Key Features  

---

#### Resource Isolation  

- Separate workloads within same cluster  
- Prevent interference between teams/apps  

---

#### Name Scoping  

- Resource names must be unique **within a namespace only**  

Example:

- `service/web` can exist in both:
  - dev  
  - prod  

---

#### Access Control  

- Use **RBAC** to restrict access per namespace  

---

#### Resource Quotas  

- Limit:

  - CPU  
  - Memory  
  - Number of objects  

---

### 3. Common Commands  

---

#### List Namespaces  

    kubectl get namespaces

---

#### Create Namespace  

    kubectl create namespace dev

---

#### Run Pod in Namespace  

    kubectl run nginx --image=nginx -n dev

---

#### Set Default Namespace  

    kubectl config set-context --current --namespace=dev

---

### 4. Use Cases  

- Separate environments:

  - dev  
  - staging  
  - prod  

- Multi-team isolation  
- System namespaces:

  - kube-system  
  - monitoring  

---

### 5. Summary  

| Feature         | Purpose                              |
|-----------------|--------------------------------------|
| Isolation       | Separate workloads                   |
| Naming          | Avoid conflicts                      |
| Access Control  | RBAC per namespace                   |
| Resource Limits | Control usage                        |

---

### 6. Key Insight  

- Namespace = **logical boundary, not physical isolation**  

---

### Interview Summary  

A Namespace in Kubernetes is a logical partition of a cluster that allows you to isolate resources, manage access using RBAC, and apply resource quotas. It is commonly used to separate environments like dev, staging, and production within the same cluster.

### Question  
What are taints and tolerations in Kubernetes?

---

### Answer  

### 1. What are Taints  

- **Taints** are applied to nodes to **repel pods**  

- Pods will **not be scheduled** unless they tolerate the taint  

---

#### Syntax  

    key=value:effect

---

#### Effects  

| Effect            | Description                                      |
|-------------------|--------------------------------------------------|
| NoSchedule        | Pod won’t be scheduled                          |
| PreferNoSchedule  | Avoid scheduling if possible                    |
| NoExecute         | Evict existing pods + prevent scheduling        |

---

#### Example  

    kubectl taint nodes node1 dedicated=database:NoSchedule

- Only pods with matching toleration can run on this node  

---

### 2. What are Tolerations  

- **Tolerations** allow pods to **run on tainted nodes**  

---

#### Example Pod  

    apiVersion: v1
    kind: Pod
    metadata:
      name: db-pod
    spec:
      tolerations:
      - key: "dedicated"
        operator: "Equal"
        value: "database"
        effect: "NoSchedule"
      containers:
      - name: mydb
        image: mysql:5.7

---

### 3. How They Work Together  

| Node           | Pod Toleration                     | Result                     |
|----------------|----------------------------------|----------------------------|
| Tainted        | Matching toleration               | Pod can schedule           |
| Tainted        | No toleration                     | Pod cannot schedule        |
| Untainted      | Any pod                           | Pod schedules normally     |

---

### 4. Common Use Cases  

---

#### Dedicated Nodes  

- Example:

  - GPU nodes for ML workloads  

---

#### Workload Isolation  

- Sensitive workloads on secure nodes  

---

#### Node Maintenance  

- Use NoExecute to evict pods  

---

### 5. Key Insight  

- Taints = **block pods**  
- Tolerations = **allow specific pods**  

---

### Interview Summary  

Taints and tolerations work together to control pod scheduling in Kubernetes. Taints are applied to nodes to repel pods, while tolerations are defined in pod specifications to allow them to be scheduled on those nodes. This mechanism is commonly used for workload isolation, dedicated nodes, and maintenance operations.

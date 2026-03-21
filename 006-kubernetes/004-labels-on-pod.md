### Question  
Need to provision big data app pods on Big Data nodes only and no other application pods should be deployed on Big Data nodes. How do we achieve it?

---

### Answer  

### 1. Label the Big Data Nodes  

First, identify nodes:

    kubectl get nodes

Add a label:

    kubectl label node <bigdata-node-name> type=bigdata

- Now these nodes are tagged for Big Data workloads  

---

### 2. Use Node Affinity in Pod Spec  

Ensure Big Data pods are scheduled **only on labeled nodes**:

    apiVersion: v1
    kind: Pod
    metadata:
      name: bigdata-app
    spec:
      containers:
      - name: app
        image: bigdata-app:latest
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: type
                operator: In
                values:
                - bigdata

- This restricts pods to **only Big Data nodes**

---

### 3. Taint Big Data Nodes  

Prevent other pods from scheduling on these nodes:

    kubectl taint nodes <bigdata-node-name> dedicated=bigdata:NoSchedule

- `NoSchedule` ensures:
  - Only pods with matching toleration can be scheduled  

---

### 4. Add Toleration to Big Data Pods  

Allow only Big Data pods to run on these tainted nodes:

    spec:
      tolerations:
      - key: "dedicated"
        operator: "Equal"
        value: "bigdata"
        effect: "NoSchedule"

- Without this → Pod will not be scheduled  

---

### 5. Combined Pod Configuration  

    apiVersion: v1
    kind: Pod
    metadata:
      name: bigdata-app
    spec:
      containers:
      - name: app
        image: bigdata-app:latest
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: type
                operator: In
                values:
                - bigdata
      tolerations:
      - key: "dedicated"
        operator: "Equal"
        value: "bigdata"
        effect: "NoSchedule"

---

### 6. Summary of Mechanism  

| Mechanism                   | Purpose                                          |
|----------------------------|--------------------------------------------------|
| Node Labels + Affinity     | Schedule pods only on specific nodes             |
| Taints + Tolerations       | Block other pods from those nodes                |

---

### 7. Key Insight  

- **Affinity = Attraction (force pods to specific nodes)**  
- **Taints = Repulsion (block unwanted pods)**  

Using both together:

- Big Data pods → **only on Big Data nodes**  
- Other pods → **cannot run on Big Data nodes**

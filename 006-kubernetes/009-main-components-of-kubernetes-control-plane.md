### Question  
What are the main components of the Kubernetes control plane?

---

### Answer  

### 1. Overview  

The **Kubernetes Control Plane** manages the cluster and ensures the system matches the **desired state**.

It handles:

- Scheduling  
- Scaling  
- State management  
- Cluster orchestration  

---

### 2. API Server (kube-apiserver)  

- Entry point to the cluster  
- Exposes Kubernetes REST API  

Responsibilities:

- Accepts requests (kubectl, APIs)  
- Authentication & authorization  
- Validates requests  
- Updates cluster state in etcd  

---

### 3. Scheduler (kube-scheduler)  

- Assigns Pods to Nodes  

Responsibilities:

- Watches for unscheduled Pods  
- Selects best node based on:
  - CPU / Memory  
  - Affinity / Anti-affinity  
  - Taints / Tolerations  
  - Policies  

---

### 4. Controller Manager (kube-controller-manager)  

- Runs multiple controllers  
- Ensures actual state = desired state  

Key Controllers:

- ReplicaSet Controller → maintains pod count  
- Deployment Controller → handles rollout/rollback  
- Node Controller → monitors node health  
- Job Controller → manages batch jobs  
- Endpoint Controller → updates service endpoints  

---

### 5. etcd (Cluster Store)  

- Distributed key-value database  

Responsibilities:

- Stores all cluster data:
  - Pods  
  - Deployments  
  - Configs  

- Acts as **source of truth**  

Important:

- Must be highly available  
- Needs backup & security  

---

### 6. Cloud Controller Manager (Optional)  

- Integrates Kubernetes with cloud providers  

Responsibilities:

- Load balancers  
- Storage volumes  
- Networking  

Examples:

- AWS  
- GCP  
- Azure  

---

### 7. Summary  

| Component                  | Role                                      |
|---------------------------|-------------------------------------------|
| API Server                | Entry point, handles requests             |
| Scheduler                 | Assigns Pods to nodes                     |
| Controller Manager        | Maintains desired state                   |
| etcd                      | Stores cluster state (source of truth)    |
| Cloud Controller Manager  | Manages cloud-specific resources          |

---

### 8. Key Insight  

- Control Plane = **Brain of Kubernetes**  
- Worker Nodes = **Execution layer**  

---

### Interview Summary  

The Kubernetes control plane consists of components like the API Server, Scheduler, Controller Manager, and etcd, which together manage cluster state, scheduling, and orchestration. The optional Cloud Controller Manager integrates Kubernetes with cloud infrastructure. These components ensure that the cluster continuously matches the desired state defined by users.

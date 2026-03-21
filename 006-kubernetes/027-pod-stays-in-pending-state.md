### Question  
New pods stay in the Pending state with error: "0/3 nodes are available: insufficient CPU and memory". How do you debug and solve this problem?

---

### Answer  

### 1. Understand the Problem  

- Scheduler cannot find a node with enough resources  

Common causes:

- Pod requests too high  
- Nodes are fully utilized  
- Namespace quotas exceeded  

---

### 2. Check Pod Resource Requests  

    kubectl get pod <pod-name> -o yaml

Look for:

    resources:
      requests:
        cpu: "500m"
        memory: "512Mi"

- Scheduler uses **requests**, not limits  

---

### 3. Check Node Capacity & Usage  

    kubectl get nodes
    kubectl describe node <node-name>
    kubectl top nodes

Verify:

- Allocatable vs requested resources  
- Node utilization levels  

---

### 4. Check Namespace Quotas  

    kubectl get resourcequota -n <namespace>
    kubectl describe resourcequota <quota-name> -n <namespace>

- Ensure quota allows new pods  

---

### 5. Check Cluster-Wide Usage  

    kubectl get pods -o wide --all-namespaces

- Identify heavy workloads  
- Check for resource-hogging pods  

---

### 6. Solutions  

---

#### A. Reduce Resource Requests  

- Lower CPU/memory requests if overestimated  

---

#### B. Scale the Cluster  

- Add more nodes  
- Enable Cluster Autoscaler  

---

#### C. Free Up Resources  

- Remove unused pods  
- Restart stuck pods  
- Rebalance workloads  

---

#### D. Use Vertical Pod Autoscaler (Optional)  

- Automatically adjust requests  

---

#### E. Optimize Workloads  

- Break large pods into smaller ones  
- Schedule non-critical jobs during off-peak  

---

### 7. Debugging Commands Summary  

| Action                      | Command                                     |
|-----------------------------|---------------------------------------------|
| Pod resources               | `kubectl get pod <pod> -o yaml`             |
| Node capacity               | `kubectl describe node <node>`              |
| Node utilization            | `kubectl top nodes`                         |
| Namespace quotas            | `kubectl get resourcequota -n <namespace>`  |
| Cluster pods                | `kubectl get pods -A -o wide`               |

---

### 8. Key Insight  

- Scheduling = **requests vs available resources**  
- If requests > available → Pod stays Pending  

---

### Interview Summary  

When pods are stuck in Pending due to insufficient CPU or memory, check resource requests, node capacity, and namespace quotas. Resolve by reducing resource requests, freeing up resources, or scaling the cluster. Proper resource planning and autoscaling help prevent such issues in production.

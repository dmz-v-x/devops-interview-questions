### Question  
What steps would you take if a node becomes unschedulable in a Kubernetes cluster?

---

### Answer  

### 1. Identify the Reason  

Start with:

    kubectl describe node <node-name>

Look for:

- `Unschedulable: true`  
- Taints (`NoSchedule`, `PreferNoSchedule`)  
- Resource pressure (Memory, Disk, PID)  

---

### 2. Check Node Taints  

    kubectl describe node <node-name>

Look under:

    Taints:

If taints are blocking scheduling:

Fix:

- Remove taint:

        kubectl taint nodes <node-name> <key>=<value>:NoSchedule-

- OR add tolerations to pods  

---

### 3. Check Node Status  

    kubectl get nodes

- Look for:
  - NotReady  
  - SchedulingDisabled  

If NotReady:

- Check kubelet logs:

        journalctl -u kubelet

- Investigate:
  - Network issues  
  - Disk issues  
  - Runtime issues  

---

### 4. Check Resource Availability  

    kubectl top node <node-name>

If resources are exhausted:

Fix:

- Remove unnecessary pods  
- Adjust resource requests/limits  
- Add more nodes (scale cluster)  

---

### 5. Inspect Pods on the Node  

    kubectl get pods -o wide --all-namespaces

- Identify pods running on that node  
- Check for failures or evictions  

---

### 6. Drain the Node (If Needed)  

Safely evict workloads:

    kubectl drain <node-name> --ignore-daemonsets

- Moves pods to other nodes  
- Helps in maintenance or recovery  

---

### 7. Cordon / Uncordon Node  

Prevent scheduling:

    kubectl cordon <node-name>

Re-enable scheduling:

    kubectl uncordon <node-name>

---

### 8. Check Control Plane (If Needed)  

If issue is cluster-wide:

- Verify scheduler & API server health  

    kubectl get componentstatuses

---

### 9. Fix Underlying Issue  

Depending on root cause:

- Restart node  
- Fix network/storage issues  
- Upgrade or patch node  
- Rejoin node to cluster if required  

---

### 10. Monitor After Fix  

- Ensure node becomes **Ready**  
- Verify pods are scheduling again  

    kubectl get nodes
    kubectl get pods -o wide

---

### 11. Summary  

| Step                | Action                              |
|--------------------|-------------------------------------|
| Describe node      | Find root cause                     |
| Check taints       | Remove or add tolerations           |
| Check status       | Identify NotReady issues            |
| Check resources    | CPU / Memory / Disk                 |
| Inspect pods       | Failures / evictions                |
| Drain node         | Safe maintenance                    |
| Cordon/Uncordon    | Control scheduling                  |
| Fix issue          | Resolve root cause                  |
| Monitor            | Ensure recovery                     |

---

### 12. Key Insight  

- Unschedulable node = **Scheduler cannot place new pods**  
- Common causes:
  - Taints  
  - Resource exhaustion  
  - Node not ready  

---

### Interview Summary  

To handle an unschedulable node, first identify the root cause using `kubectl describe node`, check for taints and resource constraints, verify node health, and inspect running pods. If needed, drain and cordon the node, fix underlying issues, and then uncordon it to restore scheduling while ensuring minimal disruption to workloads.

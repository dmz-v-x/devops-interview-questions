### Question  
How can you restrict access to a DB pod to only one app in the same namespace?

---

### Answer  

Create a Kubernetes NetworkPolicy that selects the database pods and allows ingress traffic only from pods with a specific label (the permitted application). All other traffic is denied once the policy is applied.

---

### Detailed explanation of the answer for readers’ understanding

By default, Kubernetes networking is open, meaning any pod can communicate with any other pod within the cluster. NetworkPolicies allow you to enforce fine-grained access control by whitelisting traffic based on labels, ports, and protocols.

---

### Step 1: Label Your Pods

Assign labels to identify the database and application pods:

```bash
kubectl label pods db-0 role=db
kubectl label pods app-0 role=api
```

- `role=db` → Database pods  
- `role=api` → Application pods allowed to connect  

---

### Step 2: Create NetworkPolicy

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-app-to-db
  namespace: my-namespace
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: api
    ports:
    - protocol: TCP
      port: 5432
```

---

### Step 3: Verify Behavior

- Allowed:
  - `app-0 → db-0` on port `5432`  

- Blocked:
  - Any other pod → `db-0`  

---

### Why This Works

| Component     | Purpose |
|---------------|--------|
| `podSelector` | Targets database pods (`role=db`) |
| `from`        | Allows only pods with `role=api` |
| `ports`       | Restricts access to specific port (5432) |
| Default deny  | Once policy exists, all other ingress is blocked unless explicitly allowed |

---

### Key Takeaways

- Kubernetes networking is open by default  
- NetworkPolicy enables:
  - Pod-level security  
  - Fine-grained access control  

---

### Interview-Ready Summary

“To restrict access to a database pod, I create a NetworkPolicy that selects the DB pods and allows ingress only from specific application pods using labels. For example, I allow traffic only from pods labeled role=api to pods labeled role=db on port 5432. Once the policy is applied, all other traffic is denied by default, ensuring secure communication within the namespace.”

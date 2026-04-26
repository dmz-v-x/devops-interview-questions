### Question  
How do various Kubernetes components interact when you run `kubectl apply` for a Pod?

---

### Answer  

When you run `kubectl apply -f pod.yaml`, the request is sent to the API server, which validates and stores the desired state in etcd. The scheduler then assigns the pod to a node, and the kubelet on that node pulls the image and starts the container using the container runtime. Networking is configured by kube-proxy and DNS via CoreDNS.

---

### Detailed explanation of the answer for readers’ understanding

Let’s break it down step-by-step:

---

### Step 1: kubectl apply -f pod.yaml

You define a Pod manifest like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: app
    image: nginx
```

You run:

```bash
kubectl apply -f pod.yaml
```

- This sends a REST request to the Kubernetes API server.

---

### Step 2: API Server receives and validates the request

- The **kube-apiserver** is the front-end of the control plane.
- It performs:
  - Authentication (who you are)
  - Authorization (are you allowed)
  - Validation (is the YAML correct)

- If valid:
  - The desired state of the Pod is stored in **etcd** (cluster’s key-value store).

---

### Step 3: Controllers observe the desired state

- Controllers continuously watch the API server (which reflects etcd state).
- The system detects:
  - A new Pod exists
  - It is not yet scheduled (no node assigned)

---

### Step 4: Scheduler assigns a node

- The **kube-scheduler**:
  - Watches for unscheduled pods  
  - Selects the best node based on:
    - Available CPU/memory  
    - Taints and tolerations  
    - Node affinity / anti-affinity  
    - Other constraints  

- It updates the Pod spec with:

```yaml
nodeName: selected-node
```

---

### Step 5: kubelet on the selected node acts

- The **kubelet** on that node:
  - Watches the API server  
  - Detects the assigned pod  

- Actions performed:
  - Pulls the container image (nginx) from registry  
  - Uses container runtime (containerd / Docker / CRI-O)  
  - Starts the container  

---

### Step 6: Container Runtime runs the container

- The container runtime:
  - Creates container  
  - Manages lifecycle  
  - Ensures process is running  

---

### Step 7: Networking is configured

- **kube-proxy**:
  - Sets up networking rules  
  - Enables Service-based routing  

- **CoreDNS**:
  - Provides DNS resolution inside cluster  
  - Allows pods/services to communicate via names  

---

### Step 8: Pod reaches Running state

- Once container starts successfully:
  - Pod status → Running  

- You can verify:

```bash
kubectl get pods
kubectl describe pod myapp
```

---

### End-to-End Flow Summary

```text
kubectl → API Server → etcd
           ↓
     Scheduler assigns node
           ↓
       kubelet pulls image
           ↓
   Container runtime starts container
           ↓
   kube-proxy + CoreDNS handle networking
           ↓
         Pod Running
```

---

### Key Takeaways

- API Server = entry point  
- etcd = source of truth  
- Scheduler = decides placement  
- kubelet = executes workload  
- Container runtime = runs container  
- kube-proxy + CoreDNS = networking  

---

### Interview-Ready Summary

“When I run kubectl apply, the request goes to the API server, which validates it and stores the desired state in etcd. The scheduler then assigns the pod to a suitable node, and the kubelet on that node pulls the image and starts the container using the container runtime. Finally, kube-proxy and CoreDNS handle networking, and the pod transitions to the running state.”

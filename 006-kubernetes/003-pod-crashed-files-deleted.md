### Question  
The nginx pod created in previous scenario crashed and the config (like index.html) was deleted. How to avoid similar events in the future?

---

### Answer  

### 1. Root Cause  

- Containers use an **ephemeral filesystem**  
- When a Pod crashes/restarts → **data inside container is lost**  

---

### 2. Use Volumes to Persist Data  

Kubernetes provides multiple ways to persist data outside the container.

---

#### a) PersistentVolume (PV) + PersistentVolumeClaim (PVC)  

Best for **dynamic or frequently changing data**

---

Step 1: Create PersistentVolume  

    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: nginx-pv
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      hostPath:
        path: /root/nginx-data

---

Step 2: Create PersistentVolumeClaim  

    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: nginx-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi

---

Step 3: Mount PVC in Pod  

    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: nginx-storage
      volumes:
      - name: nginx-storage
        persistentVolumeClaim:
          claimName: nginx-pvc

---

Result:

- Data stored in `/usr/share/nginx/html` persists  
- Survives Pod restarts and crashes  

---

#### b) Use ConfigMap for Static Files  

Best for **static HTML/config files**

---

Create ConfigMap:

    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: nginx-html
    data:
      index.html: |
        <h1>Hello from ConfigMap!</h1>

---

Mount in Pod:

    volumeMounts:
    - name: html-volume
      mountPath: /usr/share/nginx/html

    volumes:
    - name: html-volume
      configMap:
        name: nginx-html

---

Result:

- Content is managed by Kubernetes  
- Survives container restarts  
- Easy to update/version  

---

#### c) HostPath Volume (For Local Testing Only)  

- Stores data on node filesystem  
- Not recommended for production  

---

### 3. Summary of Approaches  

| Approach               | Use Case                            | Pros                                | Cons                        |
|----------------------|-------------------------------------|-------------------------------------|-----------------------------|
| PersistentVolume + PVC | Dynamic / changing data             | Durable, survives restarts          | Requires storage setup      |
| ConfigMap             | Static HTML / config                | Easy, version-controlled            | Not for large/dynamic data  |
| HostPath              | Local testing                      | Simple                              | Not portable, node-dependent|

---

### 4. Key Takeaway  

- Never store important data inside container filesystem  
- Use:
  - **PVC → dynamic data**  
  - **ConfigMap → static content**  

---

### 5. Interview Insight  

Why did data get deleted?

- Because containers are **stateless by default**  
- Restart = fresh filesystem  

How to fix?

- Use **persistent storage (Volumes)** instead of container storage  

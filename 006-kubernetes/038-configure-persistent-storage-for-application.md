### Question  
You have a stateful application that requires persistent storage in Kubernetes. How would you configure persistent storage for this application?

---

### Answer  

### 1. Use PersistentVolume (PV) & PersistentVolumeClaim (PVC)  

- **PV** → actual storage (EBS, NFS, etc.)  
- **PVC** → request for storage by application  

- Ensures data persists across Pod restarts  

---

### 2. Use StorageClass (Dynamic Provisioning)  

- Automatically provisions storage  

Example:

    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: gp2
    provisioner: kubernetes.io/aws-ebs
    parameters:
      type: gp2
    reclaimPolicy: Retain
    volumeBindingMode: WaitForFirstConsumer

---

### 3. Create PersistentVolumeClaim (PVC)  

    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: myapp-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi
      storageClassName: gp2

---

### 4. Use StatefulSet for Stateful Apps  

- Ensures:

  - Stable identity  
  - Dedicated storage per replica  

Example:

    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: mydb
    spec:
      serviceName: "mydb"
      replicas: 3
      selector:
        matchLabels:
          app: mydb
      template:
        metadata:
          labels:
            app: mydb
        spec:
          containers:
          - name: db
            image: mysql:8
            ports:
            - containerPort: 3306
            volumeMounts:
            - name: data
              mountPath: /var/lib/mysql
      volumeClaimTemplates:
      - metadata:
          name: data
        spec:
          accessModes: ["ReadWriteOnce"]
          storageClassName: gp2
          resources:
            requests:
              storage: 10Gi

---

### 5. How It Works  

- Each Pod gets its own PVC:

    data-mydb-0  
    data-mydb-1  
    data-mydb-2  

- Data persists even if Pods restart  

---

### 6. Access Modes  

- ReadWriteOnce → single node  
- ReadOnlyMany → multiple readers  
- ReadWriteMany → multiple writers (special storage)  

---

### 7. Important Considerations  

---

#### Storage Type  

- SSD → high performance  
- HDD → cost-effective  

---

#### Reclaim Policy  

- Retain → keep data after deletion  
- Delete → remove storage  

---

#### Backup & Recovery  

- Use:

  - Snapshots  
  - Velero  

---

### 8. Summary  

| Component       | Purpose                          |
|-----------------|----------------------------------|
| StorageClass    | Defines storage type             |
| PVC             | Requests storage                 |
| PV              | Actual storage                   |
| StatefulSet     | Manages stateful pods            |

---

### 9. Key Insight  

- Stateful apps require:
  - Persistent storage  
  - Stable identity  
  - Ordered management  

---

### Interview Summary  

To configure persistent storage for a stateful application, use a StorageClass for dynamic provisioning, define PVCs for storage requests, and deploy the application using a StatefulSet with volumeClaimTemplates. This ensures each replica gets its own persistent storage that survives restarts and maintains data integrity.

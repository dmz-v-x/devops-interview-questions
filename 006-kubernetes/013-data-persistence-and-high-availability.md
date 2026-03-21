### Question  
You are tasked with deploying a stateful application on Kubernetes. How would you ensure data persistence and high availability?

---

### Answer  

### 1. Persistent Storage (PVs & PVCs)  

- Use **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)**  

Purpose:

- Ensure data survives:
  - Pod restarts  
  - Rescheduling  
  - Crashes  

Example:

    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: my-pvc
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 10Gi

---

### 2. Use StatefulSets  

- Designed for **stateful applications**  

Provides:

- Stable Pod identity  
- Stable storage  
- Ordered deployment  

Example:

    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: my-stateful-app
    spec:
      serviceName: "my-stateful-app"
      replicas: 3
      selector:
        matchLabels:
          app: my-stateful-app
      template:
        metadata:
          labels:
            app: my-stateful-app
        spec:
          containers:
            - name: my-container
              image: my-app-image
              volumeMounts:
                - name: my-storage
                  mountPath: /data
      volumeClaimTemplates:
        - metadata:
            name: my-storage
          spec:
            accessModes: [ "ReadWriteOnce" ]
            resources:
              requests:
                storage: 10Gi

---

### 3. StorageClass (Dynamic Provisioning)  

- Automates volume creation  

Example:

    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: high-availability-storage
    provisioner: kubernetes.io/aws-ebs
    parameters:
      type: gp2
      fsType: ext4

---

### 4. High Availability (HA) Strategy  

---

#### Multiple Replicas  

- Use odd number (3, 5)

Benefits:

- Fault tolerance  
- Continuous availability  

---

#### Pod Anti-Affinity  

- Spread Pods across nodes  

    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            - labelSelector:
                matchExpressions:
                  - key: app
                    operator: In
                    values:
                      - my-stateful-app
              topologyKey: kubernetes.io/hostname

---

### 5. Data Replication  

- Use application-level replication  

Examples:

- MySQL replication  
- PostgreSQL streaming  
- MongoDB replica set  

- Ensures:
  - Data redundancy  
  - Failover capability  

---

### 6. Backup Strategy  

- Regular backups of PVs  

Tools:

- Velero  
- Cloud snapshots  

Example:

- Volume snapshot backups  

---

### 7. Health Checks  

- Configure probes:

    livenessProbe  
    readinessProbe  

Purpose:

- Restart unhealthy pods  
- Ensure traffic only to healthy pods  

---

### 8. Monitoring & Alerting  

- Use:

  - Prometheus  
  - Grafana  

Monitor:

- Pod health  
- Storage usage  
- Replication status  

---

### 9. Disaster Recovery  

- Multi-zone deployment  

Benefits:

- Survive node/zone failures  

- Restore using backups  

---

### 10. Summary  

| Area                | Solution                                |
|---------------------|------------------------------------------|
| Persistence         | PV + PVC                                 |
| Workload            | StatefulSet                              |
| Storage             | StorageClass                             |
| Availability        | Replicas + Anti-affinity                 |
| Data Safety         | Replication + Backups                    |
| Reliability         | Health checks                            |
| Observability       | Monitoring & Alerts                      |
| Recovery            | Multi-zone + Restore                     |

---

### 11. Key Insight  

- Stateless apps → easy scaling  
- Stateful apps → require:
  - Storage  
  - Identity  
  - Replication  

---

### Interview Summary  

To deploy a stateful application, use StatefulSets with Persistent Volumes to ensure data persistence, combined with StorageClasses for dynamic provisioning. Achieve high availability through multiple replicas, anti-affinity rules, and application-level replication. Add backups, monitoring, and multi-zone deployment to ensure resilience and disaster recovery. 

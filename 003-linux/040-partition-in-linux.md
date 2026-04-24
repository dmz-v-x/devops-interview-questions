### Question  
How can we list and manage partitions in Linux?

---

### Answer  

---

### 1. What are Partitions in Linux

- A partition is a **logically separated section** of a physical storage device (HDD/SSD)  
- Each partition can have:
  - Its own filesystem (ext4, xfs, etc.)  
  - Its own mount point  

---

#### Why partitions are used:

- Organize data  
- Isolate OS, applications, and logs  

---

### 2. Uses of Partitions

- Separate OS and data  
- Use multiple filesystems  
- Create swap space  
- Improve security and isolation  
- Enhance performance by separating workloads  

---

### 3. When to Use Partitions

- Production Linux servers  
- Databases, web servers, CI/CD pipelines  
- Backup and snapshot strategies  

---

### 4. Advantages of Partitions

| Advantage        | Description                                                 |
| ---------------- | ----------------------------------------------------------- |
| Isolation        | Fault in one partition doesn’t affect others                |
| Security         | Limit user permissions                                      |
| Backup & Restore | Easier to manage backups                                    |
| Performance      | Reduces I/O contention                                      |
| Flexibility      | Different mount options (read-only, noexec, etc.)           |

---

### 5. DevOps Use Cases

---

#### Separate `/var` or `/opt`
- Logs, builds, binaries stored separately  
- Prevents system crashes due to disk full  

---

#### Dedicated `/home`
- User data isolation  

---

#### Swap Partition
- Provides virtual memory  

---

#### Persistent Storage
- Used for Docker volumes / Kubernetes PV  

---

#### Backup & Snapshots
- Easier with separate partitions  

---

### 6. How to List Partitions (IMPORTANT)

---

#### 6.1 Using `lsblk` (Most Common)

```bash
lsblk
```

- Shows:
  - Disks  
  - Partitions  
  - Mount points  

---

#### 6.2 Using `fdisk`

```bash
sudo fdisk -l
```

- Lists all partitions with details  

---

#### 6.3 Using `df`

```bash
df -h
```

- Shows mounted partitions and usage  

---

### 7. How to Create and Manage Partitions

---

### Step 1: View Existing Partitions

```bash
lsblk
fdisk -l
df -h
```

---

### Step 2: Create a New Partition

```bash
sudo fdisk /dev/sdb
```

Inside fdisk:
- `n` → New partition  
- `p` → Primary  
- `1` → Partition number  
- Set size (`+10G`)  
- `w` → Write changes  

---

### Step 3: Format the Partition

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

### Step 4: Mount the Partition

```bash
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data
df -h
```

---

### Step 5: Make it Persistent

Edit `/etc/fstab`:

```
/dev/sdb1   /mnt/data  ext4  defaults  0 2
```

---

### Step 6: Set Permissions

```bash
sudo chown jenkins:jenkins /mnt/data
sudo chmod 755 /mnt/data
```

---

### 8. Example: Jenkins Build Storage

```bash
sudo mkdir /jenkins_builds
sudo mount /dev/sdb1 /jenkins_builds
sudo chown -R jenkins:jenkins /jenkins_builds
```

- Configure Jenkins to use `/jenkins_builds`  

#### Benefit:
- Prevents `/var` from filling up  

---

### 9. Advanced DevOps Use Cases

---

### 9.1 LVM (Logical Volume Management)

```bash
sudo pvcreate /dev/sdb
sudo vgcreate data_vg /dev/sdb
sudo lvcreate -L 50G -n jenkins_lv data_vg
sudo mkfs.ext4 /dev/data_vg/jenkins_lv
sudo mount /dev/data_vg/jenkins_lv /jenkins_builds
```

#### Benefit:
- Dynamic resizing  

---

### 9.2 Docker / Kubernetes Storage

- Use partitions for:
  - Docker volumes  
  - Kubernetes Persistent Volumes  

---

### 10. Key Takeaways

- Use `lsblk`, `fdisk -l`, `df -h` to list partitions  
- Partitioning improves performance and isolation  
- Essential for DevOps workloads  
- LVM provides flexibility  

---

### 11. Interview-Ready Summary

“To list partitions in Linux, I use commands like lsblk, fdisk -l, and df -h. lsblk gives a clear hierarchical view, fdisk shows detailed partition info, and df shows mounted filesystems. Partitions are important for isolating workloads, improving performance, and managing storage efficiently in production systems.”

### Question  
Mounting an EBS Volume

---

### 1. Overview

After attaching an EBS volume, you must:
- Detect the disk  
- Format it (if new)  
- Mount it  
- (Optional) Persist it across reboots  

---

### 2. Connect to EC2 Instance

```bash
ssh -i your-key.pem ec2-user@your-ec2-public-ip
```

---

### 3. Step-by-Step Process

---

### 3.1 List Attached Devices

```bash
lsblk
```

#### Example Output:
```
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   30G  0 disk /
xvdf    202:80   0   10G  0 disk
```

- `/dev/xvda` → Root volume  
- `/dev/xvdf` → New EBS volume (no mountpoint yet)  

---

### 3.2 Format the New Volume

```bash
sudo mkfs -t ext4 /dev/xvdf
```

#### Important:
- Only do this if the volume is **new and empty**  
- Formatting deletes existing data  

---

### 3.3 Create a Mount Point

```bash
sudo mkdir /mnt/mydata
```

---

### 3.4 Mount the Disk

```bash
sudo mount /dev/xvdf /mnt/mydata
```

---

### 3.5 Verify the Mount

```bash
df -h
```

#### Example Output:
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvdf        10G   24M   10G   1% /mnt/mydata
```

---

### 4. Make Mount Persistent (Optional but Recommended)

---

### 4.1 Get UUID of Volume

```bash
sudo blkid /dev/xvdf
```

#### Example Output:
```
/dev/xvdf: UUID="abc123-..." TYPE="ext4"
```

---

### 4.2 Edit fstab

```bash
sudo nano /etc/fstab
```

#### Add entry:
```
UUID=abc123-...  /mnt/mydata  ext4  defaults,nofail  0  2
```

---

### 4.3 Test fstab Entry

```bash
sudo mount -a
```

#### If no errors:
- Mount will persist after reboot  

---

### 5. Key Takeaways

- Use `lsblk` to identify disks  
- Format only new volumes  
- Mount using `mount` command  
- Use UUID in `/etc/fstab` for persistence  
- Always test with `mount -a`  

---

### 6. Interview-Ready Summary

“After attaching an EBS volume, I SSH into the instance and use lsblk to identify the new disk. If it’s a new volume, I format it using mkfs, create a mount directory, and mount it. Then I verify using df -h. To make it persistent, I add the UUID entry to /etc/fstab and test it using mount -a to ensure it mounts automatically after reboot.”

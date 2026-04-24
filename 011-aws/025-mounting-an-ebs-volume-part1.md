### Question  
Mounting an EBS Volume 

---

### 1. Overview

When you create or attach a new **EBS volume** to an EC2 instance:
- It is **not automatically usable**
- You must:
  1. Attach it  
  2. Format it (if new)  
  3. Mount it  

---

## PART 1: Create & Attach EBS Volume (AWS Console)

---

### Step 1: Go to Volumes

- Open EC2 Dashboard  
- Navigate:
  - Left sidebar → **Volumes (Elastic Block Store)**  

---

### Step 2: Create a New Volume

- Click **Create Volume**

#### Choose:
- Volume type (gp3, gp2, etc.)  
- Size (e.g., 10 GiB)  
- Availability Zone:
  - Must match EC2 instance AZ (e.g., `us-east-1a`)  

- Click **Create Volume**

---

### Step 3: Attach Volume to EC2

- Select the created volume  
- Click:
  - **Actions → Attach Volume**  

#### Choose:
- Instance  
- Device name (e.g., `/dev/sdf`)  

---

## PART 2: Configure Volume Inside EC2

---

### Step 4: Connect to EC2 Instance

```bash
ssh -i key.pem ec2-user@<public-ip>
```

---

### Step 5: Check Attached Disk

```bash
lsblk
```

#### Example Output:
- `/dev/xvdf` → New volume  

---

### Step 6: Format the Volume (First Time Only)

```bash
sudo mkfs -t ext4 /dev/xvdf
```

---

### Step 7: Create Mount Directory

```bash
sudo mkdir /mnt/mydata
```

---

### Step 8: Mount the Volume

```bash
sudo mount /dev/xvdf /mnt/mydata
```

---

### Step 9: Verify Mount

```bash
df -h
```

---

## PART 3: Persist Mount After Reboot

---

### Step 10: Get UUID of Volume

```bash
sudo blkid
```

---

### Step 11: Edit fstab

```bash
sudo nano /etc/fstab
```

#### Add entry:
```
UUID=<your-uuid> /mnt/mydata ext4 defaults,nofail 0 2
```

---

### Step 12: Test fstab Entry

```bash
sudo mount -a
```

---

## 4. Key Takeaways

- EBS volume must be:
  - Attached  
  - Formatted  
  - Mounted  

- Use `lsblk` to identify disks  
- Use `fstab` for persistence  
- Always match AZ during creation  

---

## 5. Interview-Ready Summary

“To mount an EBS volume, I first create it in the same availability zone as the EC2 instance and attach it. Then I connect to the instance, identify the new disk using lsblk, format it using mkfs if it’s new, and mount it to a directory. Finally, I update /etc/fstab using the volume’s UUID to ensure the mount persists after reboot.”

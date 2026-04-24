### Question  
EC2 instance running out of disk space — How would you troubleshoot and fix it?

---

### 1. Overview

Disk space issues in EC2 can lead to:
- Application failures  
- SSH access issues  
- System instability  

A combination of **cleanup and scaling storage** is required.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Disk Usage

```bash
df -h
```

#### Purpose:
- Identify which filesystem is full  

---

### 2.2 Identify Large Files

```bash
du -sh /* | sort -h
```

#### Purpose:
- Find directories consuming the most space  

---

### 2.3 Check Logs

- Common location:
```bash
/var/log
```

#### Actions:
- Delete old logs  
- Archive or move logs to S3  

---

### 2.4 Clean Temporary Files

```bash
rm -rf /tmp/*
```

- Remove unused cache files  
- Clean package manager cache  

---

### 3. Extend Disk Volume (Permanent Fix)

---

### 3.1 Modify Volume in AWS

- Go to:
  - EC2 → Volumes → Select Volume → Modify Volume  
- Increase size  

---

### 3.2 Resize Filesystem

After volume expansion:

```bash
sudo resize2fs /dev/xvdf
```

*(Device name may vary, e.g., /dev/xvda1)*

---

### 4. Additional Checks

- Remove unused Docker images:
```bash
docker system prune -af
```

- Clear old application data  
- Check for runaway processes generating logs  

---

### 5. Key Takeaways

- Always monitor disk usage proactively  
- Clean unnecessary files first  
- Extend volume when needed  
- Resize filesystem after volume expansion  

---

### 6. Interview-Ready Summary

“If an EC2 instance runs out of disk space, I first check usage using df -h and identify large files using du. I clean up unnecessary logs and temporary files, often under /var/log or /tmp. If more space is required, I extend the EBS volume from the AWS console and then resize the filesystem using resize2fs. This ensures both immediate resolution and long-term stability.”

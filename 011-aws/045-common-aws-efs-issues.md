### Question  
What are common AWS EFS issues and how would you troubleshoot and resolve them?

---

### Answer  

---

### 1. EFS Not Mounting

---

#### Symptoms

- `mount.nfs4: Connection timed out`  
- EC2/ECS unable to mount EFS  

---

#### Causes

- Missing mount targets in AZ  
- Security group misconfiguration  
- Incorrect DNS usage  

---

#### Fix

- Ensure:
  - Mount targets exist in all required AZs  
  - Security groups allow:
    - EC2 → outbound TCP 2049  
    - EFS → inbound TCP 2049  

- Use DNS:

```text
fs-xxxx.efs.<region>.amazonaws.com
```

- Test:

```bash
telnet fs-xxxx.efs.<region>.amazonaws.com 2049
```

---

### 2. Slow Performance / High Latency

---

#### Symptoms

- Slow file operations  
- Low throughput  

---

#### Causes

- Wrong performance mode  
- Bursting limits exceeded  
- Many small file operations  

---

#### Fix

- Choose correct mode:
  - General Purpose → low latency  
  - Max I/O → higher scalability  

- Use:
  - Provisioned throughput  

- Optimize:
  - Use `amazon-efs-utils`  
  - Tune NFS options  

- Optional:
  - Use EFS One Zone (lower latency)  

---

### 3. High Cost

---

#### Symptoms

- Unexpectedly high billing  

---

#### Causes

- Data accumulation  
- Using Standard storage for infrequent data  

---

#### Fix

- Enable Lifecycle Management:
  - Move data → IA storage  

- Clean up:
  - Old/unused files  

- Use:
  - EFS One Zone (if acceptable)  

- Monitor:
  - Cost Explorer  
  - CloudWatch  

---

### 4. Permission Denied Issues

---

#### Symptoms

- Mount works, but access denied  

---

#### Causes

- POSIX permissions mismatch  
- Incorrect UID/GID  

---

#### Fix

```bash
chown -R <user>:<group> /mount-point
chmod -R 755 /mount-point
```

- Ensure:
  - Correct UID/GID mapping  

- Optional:
  - Use IAM authorization with `-o iam`  

---

### 5. Cross-Region / Cross-Account Access

---

#### Symptoms

- Cannot access EFS across regions/accounts  

---

#### Causes

- EFS is region-specific  
- Missing IAM/resource policies  

---

#### Fix

- Cross-region:
  - Use AWS DataSync  
  - Replicate via S3  

- Cross-account:
  - Configure IAM + EFS resource policies  

---

### 6. Lambda / ECS Cold Start Delays

---

#### Symptoms

- Slow startup times  

---

#### Causes

- EFS mount during initialization  

---

#### Fix

- Use:
  - Lambda provisioned concurrency  

- Keep:
  - ECS tasks warm  

- Optimize:
  - Cache frequently used data locally  

---

### 7. Best Practices

- Deploy:
  - Mount targets in each AZ  

- Secure:
  - Allow only TCP 2049  

- Use:
  - `amazon-efs-utils`  

- Enable:
  - Lifecycle management  

- Use:
  - Access Points for isolation  

- Monitor:
  - CloudWatch (throughput, burst credits)  

---

### 8. Key Takeaways

- Most issues come from:
  - Networking  
  - Permissions  
  - Misconfiguration  

- Always validate:
  - SG + NACL  
  - Mount targets  
  - Performance settings  

---

### 9. Interview-Ready Summary

“Common EFS issues include mount failures due to security group or mount target misconfiguration, performance problems due to incorrect throughput modes, high costs from unmanaged storage growth, and permission errors due to POSIX mismatches. I troubleshoot by checking networking, mount targets, and logs, and resolve issues by configuring security groups correctly, optimizing performance modes, enabling lifecycle policies, and ensuring proper permissions. I also follow best practices like using access points, monitoring with CloudWatch, and deploying mount targets across AZs.”

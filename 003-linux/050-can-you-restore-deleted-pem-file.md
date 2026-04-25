### Question  
Can you restore a lost PEM file? If not, how can you still access the EC2 instance?

---

### Answer  

---

### 1. Can You Restore a Lost PEM File?

- **No**, you cannot restore a lost PEM file  
- AWS does **not store or allow retrieval** of private keys after creation  

---

### 2. Impact

- You cannot SSH using the old key  
- Instance is still running, but access is lost  

---

### 3. How to Regain Access (Recovery Process)

---

### Step 1: Create a New Key Pair

```bash
aws ec2 create-key-pair \
  --key-name new-key \
  --query 'KeyMaterial' \
  --output text > new-key.pem

chmod 400 new-key.pem
```

---

### Step 2: Stop the Instance

```bash
aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxxxxx
```

---

### Step 3: Detach Root Volume

- Go to:
  - EC2 → Volumes  
- Detach root volume (`/dev/xvda`)  

---

### Step 4: Attach to Temporary Instance

- Attach as secondary volume:
```
/dev/xvdf
```

---

### Step 5: Mount the Volume

```bash
sudo mkdir /mnt/recovery
sudo mount /dev/xvdf1 /mnt/recovery
```

---

### Step 6: Update `authorized_keys`

```bash
sudo nano /mnt/recovery/home/ec2-user/.ssh/authorized_keys
```

- Add:
  - Public key from new key pair  

---

### Step 7: Reattach Volume

- Unmount:

```bash
sudo umount /mnt/recovery
```

- Detach from rescue instance  
- Attach back to original instance as `/dev/xvda`  

---

### Step 8: Start and SSH

```bash
aws ec2 start-instances --instance-ids i-xxxxxxxxxxxxxxx

ssh -i new-key.pem ec2-user@<public-ip>
```

---

### 4. Alternative (If Available)

- Use **EC2 Instance Connect** (for supported AMIs)  
- Use **SSM Session Manager** (if IAM role is configured)  

---

### 5. Prevention Best Practices

- Backup PEM files securely  
- Use multiple access methods:
  - Secondary users  
  - IAM + SSM  
- Avoid single point of failure  

---

### 6. Key Takeaways

- PEM file is **not recoverable**  
- Access can be restored via:
  - Volume rescue method  
- Always plan backup access  

---

### 7. Interview-Ready Summary

“No, a lost PEM file cannot be restored because AWS does not store private keys. To regain access, I create a new key pair, detach the root volume, attach it to another instance, update the authorized_keys file with the new public key, and then reattach the volume. Alternatively, I can use SSM Session Manager or EC2 Instance Connect if configured.”

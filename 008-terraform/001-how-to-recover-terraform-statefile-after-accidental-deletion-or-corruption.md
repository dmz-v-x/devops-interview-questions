### Question  
How would you recover Terraform state after accidental deletion or corruption?

---

### Answer

Recovering Terraform state is critical because the state file maps your infrastructure to your configuration. If it’s lost or corrupted, Terraform loses track of resources.

Below are **all possible recovery approaches step by step**:

---

### 1. Check for Backups (First and Best Option)

Terraform itself doesn’t automatically back up state locally, but **remote backends often do**.

#### Remote Backend with Versioning (e.g., AWS S3)

If using S3 with versioning:

- Go to AWS S3 console  
- Navigate to the bucket storing the state file  
- Open the **Versions tab**  
- Restore a previous version  

#### Terraform Cloud / Enterprise

- Go to workspace → State history  
- Restore previous state  

#### Local Backup

- If you maintain backups → simply restore latest `.tfstate` file  

---

### 2. Use `terraform refresh` (For Partial Corruption)

If state is **partially corrupted but still exists**:

```bash
terraform refresh
```

#### What it does:

- Queries cloud provider APIs  
- Updates state to match real infrastructure  

#### Limitation:

- Won’t work if state file is completely deleted  

---

### 3. Recreate State Using `terraform import`

If state is **completely deleted and no backup exists**:

#### Steps:

1. Recreate Terraform configuration  
2. Import each resource manually  

```bash
terraform import <resource_type>.<resource_name> <resource_id>
```

#### Example:

```bash
terraform import aws_instance.example i-1234567890abcdef0
```

#### Notes:

- Must match configuration exactly  
- Time-consuming for large infra  
- Use `terraform plan` to validate  

---

### 4. Recover from Remote Storage (If Enabled)

If using remote backends like:

- AWS S3  
- Azure Blob Storage  
- GCS  
- Terraform Cloud  

#### Example: S3 Versioning

- Open S3 console  
- Navigate to `.terraform/` or bucket  
- Find older versions of `terraform.tfstate`  
- Restore required version  

---

### 5. Rebuild Infrastructure + Import (Last Resort)

If everything is lost:

#### Steps:

1. Manually recreate infrastructure  
2. Import resources again using:

```bash
terraform import
```

#### Consideration:

- Very time-consuming  
- Error-prone  
- Only use if no recovery possible  

---

### 6. Use `terraform state` Commands (Partial Recovery)

If only **some parts of state are broken**:

#### List resources:

```bash
terraform state list
```

#### Remove invalid entries:

```bash
terraform state rm <resource>
```

#### Add resource back:

```bash
terraform state add <resource> <resource_id>
```

Useful for fixing **inconsistent or partially broken state**.

---

### 7. Prevent Future Issues (Important)

After recovery, implement best practices:

#### Enable State Locking

- Use S3 + DynamoDB  
- Or Terraform Cloud  

Prevents concurrent modifications.

#### Enable Versioning

- Always enable versioning in S3 or storage backend  

#### Take Regular Backups

- Automate backups  
- Store securely  

---

### Quick Summary

| Situation                     | Solution                          |
|------------------------------|----------------------------------|
| Backup available             | Restore from backup              |
| Partial corruption           | `terraform refresh`              |
| No state, infra exists       | `terraform import`               |
| Remote backend               | Restore versioned state          |
| Nothing available            | Recreate + import                |
| Partial inconsistencies      | `terraform state` commands       |

---

### Interview-Ready Summary

“If Terraform state is lost or corrupted, I first check remote backend backups like S3 versioning or Terraform Cloud state history. If unavailable, I use `terraform refresh` for partial recovery or `terraform import` to rebuild state. For severe cases, I recreate infrastructure and import it. To prevent this, I always use remote backends with versioning and state locking.” 

### Question  
How to create and configure an S3 bucket using AWS CLI for storing application logs?

---

### Answer  

Here’s a clear, step-by-step approach to create and configure an S3 bucket for storing application logs using AWS CLI:

---

### 1. Create an S3 Bucket

```bash
aws s3api create-bucket \
  --bucket my-app-logs-bucket \
  --region us-east-1 \
  --create-bucket-configuration LocationConstraint=us-east-1
```

- Bucket names must be **globally unique**  
- Replace `my-app-logs-bucket` with your own  

---

### 2. Enable Versioning (Optional but Recommended)

```bash
aws s3api put-bucket-versioning \
  --bucket my-app-logs-bucket \
  --versioning-configuration Status=Enabled
```

- Helps recover deleted or overwritten logs  

---

### 3. Block Public Access (Security Best Practice)

```bash
aws s3api put-public-access-block \
  --bucket my-app-logs-bucket \
  --public-access-block-configuration '{
    "BlockPublicAcls": true,
    "IgnorePublicAcls": true,
    "BlockPublicPolicy": true,
    "RestrictPublicBuckets": true
  }'
```

- Ensures logs are **not publicly accessible**  

---

### 4. Enable Server-Side Encryption (SSE-S3)

```bash
aws s3api put-bucket-encryption \
  --bucket my-app-logs-bucket \
  --server-side-encryption-configuration '{
    "Rules": [
      {
        "ApplyServerSideEncryptionByDefault": {
          "SSEAlgorithm": "AES256"
        }
      }
    ]
  }'
```

- Encrypts logs at rest  

---

### 5. Configure Bucket Policy (Restrict Access)

```bash
aws s3api put-bucket-policy \
  --bucket my-app-logs-bucket \
  --policy '{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Principal": {"AWS": "arn:aws:iam::123456789012:role/app-logging-role"},
        "Action": "s3:PutObject",
        "Resource": "arn:aws:s3:::my-app-logs-bucket/*"
      }
    ]
  }'
```

- Allows only specific IAM role/user to write logs  

---

### 6. Configure Lifecycle Policy (Optional for Cost Optimization)

```bash
aws s3api put-bucket-lifecycle-configuration \
  --bucket my-app-logs-bucket \
  --lifecycle-configuration '{
    "Rules": [
      {
        "ID": "MoveLogsToGlacier",
        "Prefix": "",
        "Status": "Enabled",
        "Transitions": [
          {
            "Days": 30,
            "StorageClass": "GLACIER"
          }
        ],
        "Expiration": {
          "Days": 365
        }
      }
    ]
  }'
```

- Moves logs to cheaper storage (Glacier)  
- Deletes old logs after retention period  

---

### 7. Key Takeaways

- Always secure logs with **block public access + encryption**  
- Use **versioning** for recovery  
- Apply **least privilege access via bucket policies**  
- Use **lifecycle rules** for cost optimization  

---

### 8. Interview-Ready Summary

“I create the S3 bucket using aws s3api create-bucket, then secure it by blocking public access and enabling server-side encryption. I enable versioning for data protection and configure lifecycle policies to optimize storage costs. Finally, I apply a bucket policy so that only the application or logging role can write logs securely.”

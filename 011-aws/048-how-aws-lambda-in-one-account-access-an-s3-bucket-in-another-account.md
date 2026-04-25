### Question  
How can an AWS Lambda in one account access an S3 bucket in another account?

---

### Answer  

---

### 1. Overview

- Cross-account access can be achieved using:
  - **STS AssumeRole (recommended)**  
  - **S3 Bucket Policy (simpler for S3-only use cases)**  

---

### 2. Approach 1: Cross-Account Role (STS AssumeRole) ✅ Recommended

---

#### Step 1: Create IAM Role in Account B

- Trust policy (allows Account A):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<AccountA-ID>:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

#### Step 2: Attach S3 Permissions to Role (Account B)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::my-bucket-in-b/*"
    }
  ]
}
```

---

#### Step 3: Allow Lambda Role in Account A to Assume Role

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "arn:aws:iam::<AccountB-ID>:role/S3CrossAccountRole"
    }
  ]
}
```

---

#### Step 4: Lambda Code (Assume Role)

```python
import boto3

def lambda_handler(event, context):
    sts = boto3.client("sts")

    assumed = sts.assume_role(
        RoleArn="arn:aws:iam::<AccountB-ID>:role/S3CrossAccountRole",
        RoleSessionName="LambdaToS3"
    )

    creds = assumed["Credentials"]

    s3 = boto3.client(
        "s3",
        aws_access_key_id=creds["AccessKeyId"],
        aws_secret_access_key=creds["SecretAccessKey"],
        aws_session_token=creds["SessionToken"]
    )

    response = s3.get_object(Bucket="my-bucket-in-b", Key="file.txt")
    data = response["Body"].read().decode("utf-8")

    print(data)
```

---

### 3. Approach 2: S3 Bucket Policy (Resource-Based Policy)

---

#### Step 1: Add Bucket Policy in Account B

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowLambdaFromAccountA",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<AccountA-ID>:role/LambdaExecRole"
      },
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::my-bucket-in-b/*"
    }
  ]
}
```

---

#### Step 2: Lambda Code (Direct Access)

```python
import boto3

def lambda_handler(event, context):
    s3 = boto3.client("s3")

    response = s3.get_object(Bucket="my-bucket-in-b", Key="file.txt")
    data = response["Body"].read().decode("utf-8")

    print(data)
```

---

### 4. Comparison

| Approach              | Pros                              | Cons                          |
|-----------------------|-----------------------------------|-------------------------------|
| STS AssumeRole        | Secure, flexible, works everywhere| Slightly more complex         |
| S3 Bucket Policy      | Simple setup                      | Limited to supported services |

---

### 5. Key Takeaways

- Use **STS AssumeRole** for:
  - Better security  
  - Cross-service flexibility  

- Use **Bucket Policy** for:
  - Simple S3-only access  

---

### 6. Interview-Ready Summary

“To allow a Lambda in one account to access an S3 bucket in another account, I can use either a cross-account IAM role with STS AssumeRole or an S3 bucket policy. The recommended approach is to create a role in the target account, allow the source account to assume it, and grant S3 permissions to that role. Alternatively, since S3 supports resource-based policies, I can directly allow the Lambda’s execution role in the bucket policy. AssumeRole is more secure and flexible, while bucket policies are simpler for S3-specific use cases.”

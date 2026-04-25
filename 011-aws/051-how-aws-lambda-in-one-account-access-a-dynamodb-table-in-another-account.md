### Question  
How can an AWS Lambda in one account access a DynamoDB table in another account?

---

### Answer  

---

### 1. Core Concept

- Cross-account access requires:
  - **IAM Role in target account (Account B)**  
  - **STS AssumeRole from source account (Account A)**  

- Flow:
  - Lambda (Account A) → Assume Role → Access DynamoDB (Account B)  

---

### 2. Step-by-Step Setup

---

### Step 1: Create IAM Role in Account B

- Trust policy (allow Account A):

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

### Step 2: Attach DynamoDB Permissions (Account B)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:UpdateItem",
        "dynamodb:Query",
        "dynamodb:Scan"
      ],
      "Resource": "arn:aws:dynamodb:us-east-1:<AccountB-ID>:table/MyTable"
    }
  ]
}
```

---

### Step 3: Allow Lambda Role in Account A

- Lambda execution role policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "arn:aws:iam::<AccountB-ID>:role/DynamoDBCrossAccountRole"
    }
  ]
}
```

---

### Step 4: Assume Role in Lambda Code

```python
import boto3

def lambda_handler(event, context):
    sts_client = boto3.client("sts")

    assumed_role = sts_client.assume_role(
        RoleArn="arn:aws:iam::<AccountB-ID>:role/DynamoDBCrossAccountRole",
        RoleSessionName="LambdaSession"
    )

    creds = assumed_role["Credentials"]

    dynamodb = boto3.client(
        "dynamodb",
        region_name="us-east-1",
        aws_access_key_id=creds["AccessKeyId"],
        aws_secret_access_key=creds["SecretAccessKey"],
        aws_session_token=creds["SessionToken"]
    )

    response = dynamodb.get_item(
        TableName="MyTable",
        Key={"id": {"S": "123"}}
    )

    return response
```

---

### 3. How It Works

1. Lambda runs in Account A  
2. Calls STS `AssumeRole`  
3. AWS validates:
   - Trust policy (Account B)  
   - IAM permissions (Account A)  

4. STS returns temporary credentials  
5. Lambda uses those credentials to access DynamoDB  

---

### 4. Key Takeaways

- DynamoDB does NOT support resource-based policies like S3  
- Must use:
  - **STS AssumeRole approach**  

- Security:
  - Temporary credentials  
  - Least privilege access  

---

### 5. Interview-Ready Summary

“To allow a Lambda in one account to access a DynamoDB table in another account, I use a cross-account IAM role. The target account creates a role with a trust policy allowing the source account to assume it and attaches DynamoDB permissions to that role. The Lambda’s execution role is granted permission to call sts:AssumeRole, and in the code, it assumes the role to obtain temporary credentials. These credentials are then used to interact with DynamoDB securely.”

### Question  
What is AWS STS?

---

### Answer  

---

### 1. Definition

- **AWS STS (Security Token Service)**:
  - Provides **temporary security credentials**  

- Credentials include:
  - Access Key  
  - Secret Key  
  - Session Token  

---

### 2. Key Characteristics

- Temporary:
  - Valid for minutes to hours  

- Secure:
  - Automatically expire  

- Used for:
  - Role-based access  
  - Delegation  
  - Cross-account access  

---

### 3. Common Use Cases

- Cross-account access  
- Federated login (SSO, IAM Identity Center)  
- Service-to-service communication  
- Temporary elevated permissions  

---

### 4. How STS Works (Workflow)

---

#### Step 1: Role in Target Account (Account B)

- Create IAM Role:
  - Trust policy → allows Account A  
  - Permissions → defines allowed actions (e.g., DynamoDB access)  

---

#### Step 2: Source Role (Account A)

- Lambda runs with:
  - Execution role  

- Must allow:

```text
sts:AssumeRole
```

---

#### Step 3: Call STS AssumeRole

```python
sts_client = boto3.client("sts")

response = sts_client.assume_role(
    RoleArn="arn:aws:iam::<AccountB-ID>:role/DynamoDBCrossAccountRole",
    RoleSessionName="LambdaSession"
)
```

---

#### Step 4: STS Validation

- Checks:
  - Trust policy (Account B role trusts Account A)  
  - IAM policy (Account A role allowed to assume role)  

---

#### Step 5: Temporary Credentials Issued

- STS returns:
  - AccessKeyId  
  - SecretAccessKey  
  - SessionToken  
  - Expiration  

---

#### Step 6: Use Temporary Credentials

```python
creds = response["Credentials"]

dynamodb = boto3.client(
    "dynamodb",
    aws_access_key_id=creds["AccessKeyId"],
    aws_secret_access_key=creds["SecretAccessKey"],
    aws_session_token=creds["SessionToken"]
)
```

- Now:
  - Requests act as **Account B role**  

---

#### Step 7: Expiration

- Credentials expire automatically  
- Must re-assume role for new session  

---

### 5. Key Concepts

- Two policy checks required:
  - **Trust Policy** → who can assume  
  - **Permission Policy** → what they can do  

---

### 6. Key Takeaways

- STS:
  - Provides short-lived credentials  
  - Improves security  
  - Enables cross-account access  

---

### 7. Interview-Ready Summary

“AWS STS is a service that provides temporary security credentials for accessing AWS resources. It allows users or services to assume roles and gain permissions defined by that role for a limited time. It’s commonly used for cross-account access, federated authentication, and secure service-to-service communication. STS improves security by eliminating the need for long-lived credentials and enforcing role-based access control.”

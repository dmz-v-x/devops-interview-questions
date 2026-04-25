### Question  
What is a trust policy in AWS IAM?

---

### Answer  

---

### 1. Definition

- A **Trust Policy** is:
  - A JSON policy attached to an **IAM Role**  
  - Defines **who can assume the role**  

---

### 2. Key Concept

- Think of it as:

```text
Trust Policy → WHO can assume the role  
Permissions Policy → WHAT the role can do  
```

---

### 3. Key Characteristics

- Attached only to:
  - IAM Roles (not users/groups)  

- Uses:
  - `sts:AssumeRole` (or similar STS actions)  

- Defines:
  - Trusted principals:
    - AWS accounts  
    - IAM users/roles  
    - AWS services  

---

### 4. Example: Cross-Account Trust Policy

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

- Meaning:
  - Account A is allowed to assume this role  

---

### 5. Example: Service Trust Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

- Meaning:
  - AWS Lambda service can assume this role  

---

### 6. How It Works

1. Entity tries to assume role  
2. AWS checks:
   - Trust Policy → Is this entity allowed?  
3. If allowed:
   - STS issues temporary credentials  
4. Then:
   - Permissions policy defines allowed actions  

---

### 7. Key Takeaways

- Trust policy controls:
  - **Access to the role**  

- Permissions policy controls:
  - **Actions after access**  

- Both are required:
  - For secure role-based access  

---

### 8. Interview-Ready Summary

“A trust policy in AWS IAM is a policy attached to a role that defines which principals are allowed to assume that role. It works together with the permissions policy, where the trust policy determines who can assume the role, and the permissions policy defines what actions can be performed once the role is assumed. It commonly uses the sts:AssumeRole action and is essential for cross-account access and service-based role assumptions.”

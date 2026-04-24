### Question  
What is the difference between IAM Users, Groups, Roles, and Policies?

---

### 1. Overview

AWS Identity and Access Management (IAM) provides a way to securely control access to AWS resources using:

- Users  
- Groups  
- Roles  
- Policies  

Each plays a different role in access management.

---

### 2. IAM User

#### Definition:
- Represents an individual or application  

#### Key Points:
- Has **long-term credentials**:
  - Username/password  
  - Access keys (Access Key ID + Secret Access Key)  
- Can be assigned:
  - Direct policies  
  - Or added to groups  

#### Example:
- A developer logging into AWS console  

---

### 3. IAM Group

#### Definition:
- A collection of IAM users  

#### Key Points:
- Used to **manage permissions collectively**  
- Users inherit permissions from the group  

#### Example:
- "Developers" group with access to EC2 and S3  

---

### 4. IAM Role

#### Definition:
- An identity that is **assumed temporarily**  

#### Key Points:
- No long-term credentials  
- Provides **temporary security credentials**  
- Used by:
  - AWS services (EC2, Lambda)  
  - Applications  
  - Cross-account access  

#### Example:
- EC2 instance assuming a role to access S3  

---

### 5. IAM Policy

#### Definition:
- A **JSON document** that defines permissions  

#### Key Points:
- Specifies:
  - Actions (what can be done)  
  - Resources (on what)  
  - Conditions (optional constraints)  
- Can be attached to:
  - Users  
  - Groups  
  - Roles  

#### Example Policy:
```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}
```

---

### 6. Key Differences

| Component     | Purpose                          | Credentials Type       | Usage Example                      |
|---------------|----------------------------------|------------------------|------------------------------------|
| IAM User      | Individual identity              | Long-term              | Developer login                    |
| IAM Group     | Collection of users              | N/A                    | Manage team permissions            |
| IAM Role      | Temporary access                 | Temporary              | EC2 accessing S3                   |
| IAM Policy    | Permission definition            | N/A                    | Define allowed/denied actions      |

---

### 7. Best Practices

- Avoid using root account  
- Use **roles instead of access keys** wherever possible  
- Assign permissions via **groups**  
- Follow **least privilege principle**  
- Rotate credentials regularly  

---

### 8. Key Takeaways

- Users = identities  
- Groups = collection of users  
- Roles = temporary access  
- Policies = permission definitions  

---

### 9. Interview-Ready Summary

“IAM Users represent individuals or applications with long-term credentials. IAM Groups are collections of users used to manage permissions collectively. IAM Roles provide temporary access and are assumed by users, services, or applications, especially for cross-account or service-based access. IAM Policies are JSON documents that define permissions and can be attached to users, groups, or roles. Together, they provide a flexible and secure access control system in AWS.”

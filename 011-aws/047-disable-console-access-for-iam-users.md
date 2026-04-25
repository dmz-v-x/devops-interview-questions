### Question  
How do you disable console access for IAM users?

---

### Answer  

---

### 1. For New IAM Users

- During user creation:

- Uncheck:
  - **“Provide user access to the AWS Management Console”**

- Enable only:
  - **Programmatic access (Access keys)**  

- Result:
  - No password created  
  - User cannot log into AWS Console  

---

### 2. For Existing IAM Users

---

#### Option A: Remove Console Password (Recommended)

- Go to:
  - IAM → Users → Select user → **Security credentials**

- Under:
  - **Console password → Remove**

- Result:
  - Console login disabled  
  - API/CLI access still works  

---

#### Option B: Disable via CLI

```bash
aws iam delete-login-profile --user-name MyUserName
```

- Removes:
  - Login profile (password)  

- Result:
  - No console access  

---

### 3. Optional: Deny via IAM Policy (Not Preferred)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "aws-portal:ViewAccount",
      "Resource": "*"
    }
  ]
}
```

- Limitation:
  - Not a clean solution  
  - User still technically has login capability  

---

### 4. Best Practices

- Prefer:
  - IAM Roles over IAM Users  

- If using IAM Users:
  - Avoid console access unless required  
  - Use MFA for console users  

- Security:
  - Rotate access keys regularly  
  - Follow least privilege principle  

---

### 5. Key Takeaways

- Best method:
  - **Remove login profile (password)**  

- Avoid:
  - Overusing IAM users  
  - Policy-based console blocking  

---

### 6. Interview-Ready Summary

“To disable console access for an IAM user, I remove their login profile, which deletes their console password and prevents them from signing into the AWS Management Console. This can be done via the IAM console or using the CLI command aws iam delete-login-profile. For new users, I simply avoid enabling console access during creation. As a best practice, I prefer using IAM roles instead of IAM users and restrict access based on least privilege.”

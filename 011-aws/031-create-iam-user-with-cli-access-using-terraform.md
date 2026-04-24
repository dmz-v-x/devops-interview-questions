### Question  
Create an AWS IAM user with CLI access using Terraform

---

### 1. Overview

To create an IAM user with **programmatic (CLI) access** using Terraform, you need to:

- Create IAM user  
- Attach permissions (policy)  
- Generate access keys  

---

### 2. Terraform Configuration

---

### 2.1 Provider Configuration

```hcl
provider "aws" {
  region = "us-east-1"
}
```

---

### 2.2 Create IAM User

```hcl
resource "aws_iam_user" "cli_user" {
  name = "cli-user"
}
```

---

### 2.3 Attach Policy (Permissions)

Example: Attach AWS managed policy (S3 Full Access)

```hcl
resource "aws_iam_user_policy_attachment" "cli_user_policy" {
  user       = aws_iam_user.cli_user.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonS3FullAccess"
}
```

---

### 2.4 Create Access Keys (CLI Access)

```hcl
resource "aws_iam_access_key" "cli_user_key" {
  user = aws_iam_user.cli_user.name
}
```

---

### 2.5 Output Access Keys (Important)

```hcl
output "access_key_id" {
  value = aws_iam_access_key.cli_user_key.id
}

output "secret_access_key" {
  value     = aws_iam_access_key.cli_user_key.secret
  sensitive = true
}
```

---

### 3. Apply Terraform

```bash
terraform init
terraform apply
```

---

### 4. Configure AWS CLI

Use generated credentials:

```bash
aws configure
```

Enter:
- Access Key ID  
- Secret Access Key  
- Region  
- Output format  

---

### 5. Security Best Practices

- Never hardcode credentials  
- Store secrets securely (Vault, Secrets Manager)  
- Use least privilege policies  
- Rotate access keys regularly  
- Prefer IAM roles over users when possible  

---

### 6. Key Takeaways

- IAM user provides programmatic access  
- Access keys enable CLI usage  
- Policies define permissions  
- Terraform automates entire setup  

---

### 7. Interview-Ready Summary

“To create an IAM user with CLI access using Terraform, I define an aws_iam_user resource, attach a policy for required permissions, and generate access keys using aws_iam_access_key. Then I output the credentials and configure them in AWS CLI. I also follow best practices like least privilege and secure storage of credentials.”

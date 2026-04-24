### Question  
What is AWS Systems Manager Parameter Store?

---

### 1. Overview

**AWS Systems Manager Parameter Store** is a service used to store:
- Configuration data  
- Application settings  
- Secrets (optionally encrypted)  

It provides a **centralized and secure way** to manage application parameters.

---

### 2. Purpose

- Store configuration values and secrets  
- Avoid hardcoding values in applications  
- Enable centralized configuration management  

---

### 3. Key Features

---

### 3.1 Store Plain Text and Encrypted Values

- Supports:
  - Plain text parameters  
  - SecureString (encrypted values)  

---

### 3.2 Encryption with AWS KMS

- Secure parameters using **AWS Key Management Service (KMS)**  
- Ensures data protection at rest  

---

### 3.3 Integration with AWS Services

- Works with:
  - EC2  
  - ECS  
  - Lambda  
  - CloudFormation  

---

### 3.4 No Automatic Rotation

- Unlike Secrets Manager  
- Secrets must be rotated manually  

---

### 3.5 Cost-Effective

- Cheaper than AWS Secrets Manager  
- Suitable for:
  - Non-sensitive data  
  - Less frequently changing secrets  

---

### 4. Parameter Tiers

- **Standard Tier**
  - Basic usage  
  - Free with limits  

- **Advanced Tier**
  - Larger size  
  - Higher throughput  
  - Additional features  

---

### 5. Example Use Cases

- Store application configuration:
  - Database URLs  
  - API endpoints  
- Store non-rotating secrets  
- Manage environment-specific settings  

---

### 6. Parameter Types

- String → Plain text  
- StringList → Comma-separated values  
- SecureString → Encrypted values  

---

### 7. Key Takeaways

- Centralized configuration management  
- Supports encryption via KMS  
- Cheaper alternative to Secrets Manager  
- No built-in secret rotation  

---

### 8. Interview-Ready Summary

“AWS Systems Manager Parameter Store is used to store configuration data and secrets in a centralized and secure way. It supports both plain text and encrypted values using AWS KMS. It integrates with services like EC2, ECS, and Lambda, making it easy to manage application configuration. Unlike Secrets Manager, it doesn’t provide automatic rotation, but it is more cost-effective and ideal for storing non-sensitive or infrequently changing data.”

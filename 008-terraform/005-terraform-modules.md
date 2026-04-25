### Question  
What are modules in Terraform and why should we use them?

---

### Answer  

---

### 1. Definition

- Terraform modules are:
  - **Reusable, self-contained sets of Terraform configuration**  

- They help:
  - Organize infrastructure  
  - Avoid code duplication  

---

### 2. Types of Modules

- **Root Module**
  - The main directory where:
    - `terraform init`
    - `terraform apply` are executed  

- **Child Module**
  - Reusable module called by:
    - Root module  
    - Another module  

---

### 3. What is a Module Internally?

- A module is simply:
  - A folder containing `.tf` files  

- It can be stored:
  - Locally  
  - In Git repositories  
  - On Terraform Registry  

---

### 4. Why Use Modules?

| Benefit             | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Reusability**     | Write once, reuse across multiple environments                              |
| **Abstraction**     | Hide complexity behind variables and outputs                                |
| **Consistency**     | Enforce standard infrastructure patterns                                    |
| **Scalability**     | Manage large infrastructure in smaller logical pieces                       |
| **Maintainability** | Update one module without affecting the entire system                       |

---

### 5. Example — Module Structure

```
modules/
  ec2-instance/
    main.tf
    variables.tf
    outputs.tf
```

---

### 6. Calling a Module

```hcl
module "my_ec2" {
  source        = "./modules/ec2-instance"
  instance_type = "t2.micro"
  ami_id        = "ami-0abcd1234"
}
```

- `source` → Path to module  
- Inputs → Passed via variables  
- Outputs → Returned from module  

---

### 7. Real-World Use Cases

- VPC module  
- EC2 module  
- RDS module  
- Kubernetes cluster module  

- Example:
  - Same VPC module used in:
    - Dev  
    - Staging  
    - Production  

---

### 8. Key Takeaways

- Modules = **building blocks of Terraform**  
- Promote:
  - Reuse  
  - Clean code  
  - Scalable infrastructure  

- Essential for:
  - Production-grade Infrastructure as Code  

---

### 9. Interview-Ready Summary

“Terraform modules are reusable, self-contained configurations that help organize infrastructure into logical components. They allow us to avoid code duplication, enforce consistency, and improve scalability. A module is simply a folder of .tf files, and we can reuse it across environments by passing different inputs. This makes infrastructure more maintainable and modular.”

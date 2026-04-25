### Question  
What is the difference between for_each and for in Terraform?

---

### Answer  

---

### 1. Core Difference

- `for_each`:
  - Used to **create multiple resource instances**  
  - Works at **infrastructure level**  

- `for`:
  - Used to **transform or generate data structures**  
  - Works at **expression/value level**  

---

### 2. Conceptual Understanding

- `for_each` → “Create multiple resources”  
- `for` → “Generate or modify data”  

---

### 3. Detailed Comparison

| Aspect              | `for_each` (meta-argument)                     | `for` (expression)                                 |
|---------------------|-----------------------------------------------|----------------------------------------------------|
| **Primary role**    | Creates multiple resource instances           | Builds or transforms values                        |
| **Where used**      | Resource, module, data blocks                 | Variables, locals, outputs, arguments              |
| **Input type**      | Map or set                                   | List, map, or set                                 |
| **Outcome**         | Multiple resources with unique addresses      | A transformed collection (no resources created)    |

---

### 4. Example — for_each (Creates Resources)

```hcl
resource "aws_s3_bucket" "logs" {
  for_each = {
    us = "us-east-1"
    eu = "eu-west-1"
    ap = "ap-southeast-1"
  }

  bucket = "app-logs-${each.key}"
  region = each.value
}
```

- Creates:
  - `aws_s3_bucket.logs["us"]`  
  - `aws_s3_bucket.logs["eu"]`  
  - `aws_s3_bucket.logs["ap"]`  

- Key point:
  - **Actual infrastructure is created multiple times**  

---

### 5. Example — for (Transforms Data)

```hcl
variable "allowed_cidrs" {
  type    = list(string)
  default = ["10.0.0.0/24", "10.1.0.0/24"]
}

locals {
  cidr_to_rule = {
    for cidr in var.allowed_cidrs :
    cidr => { protocol = "tcp", port = 22 }
  }
}
```

- Output:

```json
{
  "10.0.0.0/24": { "protocol": "tcp", "port": 22 },
  "10.1.0.0/24": { "protocol": "tcp", "port": 22 }
}
```

- Key point:
  - **No resources created**, only data transformation  

---

### 6. How They Work Together

- Common pattern:

```hcl
locals {
  users_map = {
    for user in var.users :
    user.name => user
  }
}

resource "aws_iam_user" "users" {
  for_each = local.users_map

  name = each.key
}
```

- Flow:
  - `for` → prepares data  
  - `for_each` → creates resources  

---

### 7. Key Takeaways

- Use `for_each` when:
  - You need **multiple infrastructure resources**  

- Use `for` when:
  - You need **data transformation or mapping**  

- They are often used **together in real-world Terraform code**  

---

### 8. Interview-Ready Summary

“for_each is a Terraform meta-argument used to create multiple resource instances from a map or set, while for is an expression used to transform or generate collections like lists or maps. for_each operates at the resource level, whereas for operates at the data level. Typically, we use for to prepare data and for_each to create scalable infrastructure.”

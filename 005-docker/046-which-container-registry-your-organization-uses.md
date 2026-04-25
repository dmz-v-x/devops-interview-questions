### Question  
Which container registry does your organization use for storing and managing container images?

---

### Answer  

---

### 1. Primary Registry Used

- We primarily use:
  - **Amazon Elastic Container Registry (ECR)**  

- Reason:
  - Seamless integration with AWS ecosystem  

---

### 2. Why Amazon ECR?

- Fully managed container registry  
- Integrated with AWS IAM for access control  
- Supports:
  - Private repositories  
  - Public repositories  

- Native integrations:
  - ECS (Elastic Container Service)  
  - EKS (Elastic Kubernetes Service)  
  - CI/CD tools like CodePipeline  

- Built-in features:
  - Image vulnerability scanning (via Amazon Inspector)  
  - Lifecycle policies for automatic cleanup  
  - Versioned image tagging  

---

### 3. Typical Workflow with ECR

```bash
aws ecr get-login-password | docker login --username AWS --password-stdin <aws_account>.dkr.ecr.<region>.amazonaws.com

docker build -t myapp .

docker tag myapp:latest <repo-url>:latest

docker push <repo-url>:latest
```

- Steps:
  - Authenticate with ECR  
  - Build Docker image  
  - Tag image  
  - Push to ECR  

---

### 4. Other Registries Used

- **Docker Hub**
  - Used for:
    - Public images  
    - Base images  

- **GitHub Container Registry (GHCR)**
  - Used for:
    - Internal projects hosted on GitHub  
  - Benefits:
    - Easy integration with GitHub Actions  
    - Token-based authentication  

---

### 5. Key Takeaways

- ECR is preferred for:
  - AWS-native environments  
  - Secure and scalable image storage  

- Other registries are used based on:
  - Project needs  
  - Hosting platform  

---

### 6. Interview-Ready Summary

“We primarily use Amazon ECR as our container registry because it integrates well with AWS services like ECS, EKS, and IAM for secure access control. It also provides features like vulnerability scanning and lifecycle policies. For public images, we use Docker Hub, and for GitHub-based projects, we sometimes use GitHub Container Registry due to its seamless integration with GitHub Actions.”

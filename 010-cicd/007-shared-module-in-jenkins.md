### Question  
What are shared modules in Jenkins?

---

### 1. Overview

Shared modules in Jenkins refer to **reusable code, configurations, and resources** that can be used across multiple Jenkins jobs or pipelines.

In modern Jenkins terminology, this concept is commonly implemented using **Shared Libraries**.

---

### 2. Why Shared Modules Are Important

- Avoid code duplication  
- Maintain consistency across pipelines  
- Simplify updates and maintenance  
- Promote standardization in CI/CD processes  

---

### 3. What Can Be Shared (Examples)

---

### 3.1 Libraries

#### Description:
- Reusable code components such as:
  - Groovy scripts  
  - Shell scripts  
  - Utility functions  

#### Use Case:
- Common build logic  
- Deployment scripts  
- Reusable pipeline steps  

---

### 3.2 Shared Jenkinsfile Logic

#### Description:
- Instead of duplicating Jenkinsfile logic in every repo, you can centralize it.

#### Example:
- Common pipeline stages like:
  - Build  
  - Test  
  - Deploy  

#### Benefit:
- One change updates all pipelines  

---

### 3.3 Plugins (Shared Usage)

#### Description:
- Plugins installed globally in Jenkins  

#### Benefit:
- No need to configure plugins per job  
- Ensures consistent functionality  

---

### 3.4 Global Variables

#### Description:
- Shared variables accessible across pipelines  

#### Examples:
- Version numbers  
- Artifact repository URLs  
- Environment variables  

#### Benefit:
- Centralized configuration management  

---

### 4. Jenkins Shared Library (Actual Implementation)

#### Structure Example:
```
(root)
 ├── vars/
 │    └── buildApp.groovy
 ├── src/
 │    └── com/example/utils.groovy
 └── resources/
```

#### Usage in Jenkinsfile:
```
@Library('my-shared-lib') _
buildApp()
```

---

### 5. Key Benefits

- Reusability across multiple projects  
- Centralized pipeline logic  
- Easier maintenance and updates  
- Cleaner and shorter Jenkinsfiles  

---

### 6. Key Takeaways

- Shared modules = reusable components in Jenkins  
- Implemented using **Shared Libraries**  
- Used for:
  - Common pipeline logic  
  - Scripts and utilities  
  - Global configurations  

---

### 7. Interview-Ready Summary

“Shared modules in Jenkins refer to reusable code and configurations that can be used across multiple jobs or pipelines. In practice, this is implemented using Jenkins Shared Libraries, where we store common pipeline logic, scripts, and global variables. This helps reduce duplication, maintain consistency, and makes CI/CD pipelines easier to manage and scale.”

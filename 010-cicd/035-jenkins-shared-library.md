### Question  
What are Jenkins Shared Libraries and how do they work?

---

### Answer  

---

### What is a Jenkins Shared Library?

A Shared Library is a Git repository (or part of one) that contains reusable Groovy code that can be included in Jenkins pipelines using the `@Library` annotation.

---

### Typical Structure

```
(root)
├── vars/
│   └── sayHello.groovy
├── src/
│   └── org/example/MyClass.groovy
├── resources/
│   └── templates/config.xml
└── README.md
```

---

### Why Use Shared Libraries?

- Avoid repeating logic in every Jenkinsfile  
- Encapsulate:
  - Business logic  
  - Deployment steps  
  - Validation code  

- Benefits:
  - Centralized updates across pipelines  
  - Reduced errors  
  - Improved collaboration  

---

### How Do They Work?

---

### Step 1: Create Library Repository

- Create a Git repo with:
  - `vars/` → global pipeline functions  
  - `src/` → reusable classes  
  - `resources/` → static files  

---

### Step 2: Configure in Jenkins

- Go to:
  - Manage Jenkins → Global Pipeline Libraries  

- Add:
  - Library name  
  - Git repository URL  

---

### Step 3: Load Library in Jenkinsfile

```groovy
@Library('my-shared-library') _
```

---

### Step 4: Use Functions or Classes

- Functions from `vars/`:
  - Directly callable  

- Classes from `src/`:
  - Imported and used  

---

### Example

---

#### vars/sayHello.groovy

```groovy
def call(String name = 'world') {
    echo "Hello, ${name}!"
}
```

---

#### Jenkinsfile

```groovy
@Library('my-shared-library') _

pipeline {
    agent any
    stages {
        stage('Greet') {
            steps {
                sayHello('Abhishek')
            }
        }
    }
}
```

---

### Benefits

- DRY (Don’t Repeat Yourself)  
- Cleaner and simpler Jenkinsfiles  
- Version-controlled code  
- Reusable across teams and projects  

---

### Key Takeaways

- Shared Libraries:
  - Centralize pipeline logic  
  - Improve maintainability  
  - Enable consistency  

---

### Interview-Ready Summary

“Jenkins Shared Libraries are reusable Groovy code stored in a Git repository that can be shared across multiple pipelines. They help avoid duplication, centralize logic, and improve maintainability. You configure the library in Jenkins, load it in the Jenkinsfile using the @Library annotation, and then use functions or classes defined in the library. This makes pipelines cleaner, more consistent, and easier to manage across teams.”

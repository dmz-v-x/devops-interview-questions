### Question  
How do you set environment variables in Jenkins?

---

### 1. Overview

Environment variables in Jenkins are used to:
- Pass configuration values  
- Control build behavior  
- Inject secrets securely  

They can be defined at different levels depending on scope and use case.

---

### 2. Global Environment Variables

#### Steps:
- Go to: **Manage Jenkins → Configure System → Global properties**  
- Check: **Environment variables**  
- Add key-value pairs  

#### Example:
```
APP_ENV=production
```

#### Scope:
- Available to **all jobs** on that Jenkins instance  

---

### 3. Per-Job Environment Variables

#### For Freestyle Jobs:

- Go to: **Configure → Build Environment → Inject environment variables**  
- Define variables  

#### Scope:
- Available only to that specific job  

---

### 4. Environment Variables in Pipeline (Jenkinsfile)

#### Example:
```groovy
pipeline {
  agent any
  environment {
    APP_ENV = 'production'
    DB_USER = credentials('db-user-secret') // secure credentials
  }
  stages {
    stage('Build') {
      steps {
        echo "Environment: ${APP_ENV}"
      }
    }
  }
}
```

#### Key Points:
- `environment {}` makes variables available to **all stages**  
- `credentials()` is used to **securely inject secrets**  

---

### 5. Setting Variables from Shell Scripts

#### Example:
```bash
export MY_VAR=value
```

#### Scope:
- Limited to that **specific shell execution context**  
- Not available globally across pipeline stages  

---

### 6. Comparison of Methods

| Method                     | Scope                | Use Case                          |
|--------------------------|---------------------|----------------------------------|
| Global Variables         | All jobs            | Common configs                   |
| Per-Job Variables        | Single job          | Job-specific configs             |
| Pipeline environment {}  | Entire pipeline     | CI/CD pipelines                  |
| Shell export             | Single step         | Temporary variables              |

---

### 7. Best Practices

- Use **Pipeline environment {}** for modern CI/CD  
- Use **credentials()** for sensitive data  
- Avoid hardcoding secrets  
- Keep global variables minimal  
- Use job-level variables for customization  

---

### 8. Key Takeaways

- Multiple ways to define environment variables in Jenkins  
- Scope depends on where variables are defined  
- Secure handling is critical for secrets  

---

### 9. Interview-Ready Summary

“In Jenkins, environment variables can be set globally from the Configure System section, per job in Freestyle configurations, or within pipelines using the environment block. For pipelines, environment variables are accessible across all stages, and sensitive data can be securely injected using the credentials() helper. Variables can also be set in shell scripts using export, but those are limited to that specific execution context.”

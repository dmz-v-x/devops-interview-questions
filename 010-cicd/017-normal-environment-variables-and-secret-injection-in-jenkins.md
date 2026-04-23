### Question  
Example showing both normal environment variables and secret injection in Jenkins Pipeline

---

### 1. Overview

In Jenkins pipelines, you can define:
- **Normal environment variables** → for non-sensitive values  
- **Secret variables** → securely injected from Jenkins Credentials Store  

Both are commonly defined using the `environment {}` block.

---

### 2. Example Pipeline

```groovy
pipeline {
  agent any

  environment {
    APP_ENV = 'production'                  // normal variable
    DB_USER = credentials('db-user-secret') // from Jenkins credentials store
    API_KEY = credentials('api-key-secret') // secure token
  }

  stages {
    stage('Build') {
      steps {
        echo "Building for environment: ${APP_ENV}"
        sh 'echo "Using DB user: $DB_USER"'
      }
    }

    stage('Deploy') {
      steps {
        sh '''
          echo "Deploying with API Key: $API_KEY"
          # Run deployment script here
        '''
      }
    }
  }
}
```

---

### 3. Explanation (Step-by-Step)

---

### 3.1 environment {} Block

- Defines variables available **globally across all stages**
- Used for both:
  - Plain variables  
  - Secure credentials  

---

### 3.2 Normal Environment Variable

```groovy
APP_ENV = 'production'
```

- Used for:
  - Environment selection  
  - Config flags  
- Safe because it does **not contain sensitive data**

---

### 3.3 Secret Injection Using credentials()

```groovy
DB_USER = credentials('db-user-secret')
API_KEY = credentials('api-key-secret')
```

- Fetches secrets from Jenkins Credentials Store  
- Injects them as environment variables  

---

### 3.4 Usage in Stages

```groovy
echo "Building for environment: ${APP_ENV}"
```

- Uses normal variable  

```bash
echo "Using DB user: $DB_USER"
```

- Uses injected credential  

---

### 4. Security Behavior

- Jenkins **automatically masks sensitive values** in logs  
- Secrets are:
  - Not stored in Jenkinsfile  
  - Not exposed in console output  

---

### 5. Key Points to Highlight (Interview)

- `environment {}` makes variables available across all stages  
- `credentials()` securely injects secrets from Jenkins Credentials Store  
- Plain variables (like `APP_ENV`) are used for non-sensitive data  
- Jenkins masks sensitive values (`DB_USER`, `API_KEY`) in logs  

---

### 6. Best Practices

- Never hardcode secrets in Jenkinsfile  
- Always use `credentials()` for sensitive data  
- Separate config (non-sensitive) and secrets clearly  
- Use least privilege credentials  

---

### 7. Interview-Ready Summary

“In Jenkins pipelines, I use the environment block to define both normal and secure variables. For non-sensitive values like environment names, I use plain variables, and for secrets like database credentials or API keys, I use the credentials() helper, which securely fetches values from the Jenkins Credentials Store. Jenkins also masks these sensitive values in logs, ensuring secure handling during pipeline execution.”

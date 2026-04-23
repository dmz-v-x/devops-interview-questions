### Question  
You need to parameterize a Jenkins job to accept user input during execution. How would you implement this?

---

### 1. Overview

Parameterized Jenkins jobs allow users to:
- Provide input at runtime  
- Customize builds dynamically  
- Reuse the same job for different scenarios  

---

### 2. Enable Parameters in Jenkins Job

#### Steps:
- Open Jenkins job → Click **Configure**  
- Check:
  ```
  This project is parameterized
  ```

---

### 2.1 Types of Parameters

| Parameter Type     | Use Case                                      |
|--------------------|----------------------------------------------|
| String Parameter   | Free text input (version, branch name)       |
| Choice Parameter   | Dropdown (dev, staging, prod)                |
| Boolean Parameter  | Yes/No input                                |
| File Parameter     | Upload file during build                    |
| Password Parameter | Secure input for secrets                    |

---

### 3. Use Parameters in Build Steps

---

### 3.1 Freestyle Project

#### Example:
```bash
echo "Deploying version: $VERSION"
./deploy.sh --env $ENV
```

#### Notes:
- Parameters are available as **environment variables**  

---

### 3.2 Pipeline (Jenkinsfile)

#### Example:
```groovy
pipeline {
    agent any

    parameters {
        string(name: 'VERSION', defaultValue: '1.0.0', description: 'Version to deploy')
        choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: 'Deployment environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests before deploy?')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building version ${params.VERSION} for ${params.ENV} environment"
            }
        }

        stage('Deploy') {
            steps {
                sh "./deploy.sh --version ${params.VERSION} --env ${params.ENV}"
            }
        }
    }
}
```

---

### 4. Triggering the Job

#### Steps:
- Click:
  ```
  Build with Parameters
  ```
- Jenkins displays input fields  
- User provides values  
- Pipeline executes using those values  

---

### 5. Key Benefits

- Dynamic and reusable pipelines  
- Reduces duplication of jobs  
- Allows user-controlled deployments  

---

### 6. Best Practices

- Use meaningful parameter names  
- Provide default values where possible  
- Use credentials plugin for secrets instead of password parameters  
- Validate inputs in pipeline logic  

---

### 7. Key Takeaways

- Enable parameterization in job config  
- Use parameters in build steps or pipelines  
- Access values via environment variables or `params`  

---

### 8. Interview-Ready Summary

“To parameterize a Jenkins job, I enable the ‘This project is parameterized’ option and define parameters like string, choice, or boolean inputs. In Freestyle jobs, these parameters are used as environment variables, and in pipelines, they are accessed using the params object. When a user triggers the job using ‘Build with Parameters’, Jenkins prompts for input, making the job flexible and reusable for different scenarios.”

### Question  
How to run a particular stage in a Jenkins Pipeline?

---

### 1. Overview

Jenkins does **not directly support running a single stage only**, but there are practical ways to achieve this:

- Using **parameters + when conditions** (most common)  
- Using **Restart from Stage** (built-in feature for reruns)  

---

### 2. Method 1: Use Parameters + `when` Conditions

#### Idea:
Control which stage runs using a parameter.

---

### 2.1 Example Pipeline

```groovy
pipeline {
    agent any

    parameters {
        string(name: 'RUN_STAGE', defaultValue: '', description: 'Stage to run')
    }

    stages {
        stage('Build') {
            when {
                expression { params.RUN_STAGE == '' || params.RUN_STAGE == 'Build' }
            }
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            when {
                expression { params.RUN_STAGE == '' || params.RUN_STAGE == 'Test' }
            }
            steps {
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            when {
                expression { params.RUN_STAGE == '' || params.RUN_STAGE == 'Deploy' }
            }
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

---

### 2.2 Behavior

- If `RUN_STAGE` is empty → **All stages run**  
- If `RUN_STAGE=Test` → **Only Test stage runs**  

---

### 2.3 Use Case

- Debugging a specific stage  
- Running partial pipelines  
- Faster iteration  

---

### 3. Method 2: Restart from Stage (Built-in Feature)

#### Purpose:
Re-run pipeline from a specific stage after failure or completion  

---

### 3.1 Requirements

- Declarative Pipeline (not Scripted)  
- Required plugins:
  - Pipeline: Declarative  
  - Pipeline: Stage View  
- Use:
```groovy
options {
    checkpoints()
}
```

---

### 3.2 Example Pipeline

```groovy
pipeline {
    agent any

    options {
        checkpoints()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

---

### 3.3 How It Works

- After pipeline execution:
  - Jenkins UI shows **"Restart from Stage"** option  
- Click on a stage → pipeline restarts from that point  

#### Note:
- Uses same parameters and environment  

---

### 4. Key Differences

| Feature                 | Description                                                     |
|------------------------|-----------------------------------------------------------------|
| Restart from stage      | Supported in Declarative Pipeline with `checkpoints()`          |
| Run only one stage      | Not directly supported → use `when` + parameters workaround     |

---

### 5. Key Takeaways

- Use parameters + `when` for flexible stage execution  
- Use Restart from Stage for re-running failed pipelines  
- Combine both for better control  

---

### 6. Interview-Ready Summary

“In Jenkins, running a specific stage directly isn’t supported, but we can achieve it using parameters and when conditions to selectively execute stages. For example, passing a parameter like RUN_STAGE allows us to run only a specific stage. Additionally, Jenkins provides a ‘Restart from Stage’ feature in Declarative Pipelines, which lets us rerun the pipeline from a particular stage after a failure. Together, these approaches provide flexibility in controlling pipeline execution.”

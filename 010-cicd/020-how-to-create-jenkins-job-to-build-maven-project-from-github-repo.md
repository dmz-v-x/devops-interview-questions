### Question  
How do you create a Jenkins job to build a Maven project from a GitHub repository?

---

### 1. Overview

Creating a Jenkins job for a Maven project involves:
- Connecting Jenkins to a GitHub repository  
- Configuring build tools (Maven, JDK)  
- Defining build steps  
- Optionally automating triggers  

---

### 2. Prerequisites

Before creating the job, ensure:

- Jenkins is installed  
- Required plugins:
  - Git Plugin (for GitHub integration)  
  - Maven Integration Plugin (or Maven installed manually)  
- JDK configured:
  - **Manage Jenkins → Global Tool Configuration**  
- Maven configured in Jenkins  
- GitHub repository URL available:
  ```
  https://github.com/user/my-maven-app.git
  ```
- Jenkins has access:
  - Public repo OR  
  - Credentials (SSH key / GitHub token)  

---

### 3. Create a New Job

#### Steps:
- Login to Jenkins  
- Click **New Item**  
- Enter job name (e.g., `maven-build-job`)  
- Select:
  - **Freestyle project** (or Pipeline for advanced use)  
- Click **OK**

---

### 4. Configure GitHub Source

#### In "Source Code Management":

- Select **Git**  
- Enter repository URL  
- Add credentials (if required)  
- Specify branch:
  ```
  */main
  ```

---

### 5. Configure Build Step (Maven)

#### In "Build" section:

- Select:
  **Invoke top-level Maven targets**  

- Choose configured Maven version  

- Add goals:
  ```
  clean install
  ```

#### What this does:
- `clean` → removes previous builds  
- `install` → compiles code, runs tests, builds artifact  

---

### 6. Add Build Triggers (Optional)

---

### 6.1 GitHub Webhook (Recommended)

- Configure webhook in GitHub:
  ```
  http://<jenkins-server>:8080/github-webhook/
  ```

- Automatically triggers build on code push  

---

### 6.2 Poll SCM

- Configure in Jenkins:
  ```
  H/5 * * * *
  ```

- Checks for changes every 5 minutes  

---

### 7. Save and Run Build

- Click **Save**  
- Click **Build Now**  

#### Result:
- Jenkins will:
  - Clone repository  
  - Run `mvn clean install`  
  - Generate artifacts in:
    ```
    target/
    ```

---

### 8. Post-Build Actions (Optional but Recommended)

- Archive artifacts:
  ```
  target/*.jar
  ```
- Publish test reports  
- Notify via email/Slack  

---

### 9. Best Practices

- Prefer **Pipeline jobs with Jenkinsfile** for maintainability  
- Store credentials securely in Jenkins Credentials Store  
- Use agents/containers for consistent builds  
- Add caching to speed up builds  
- Enable parallel testing where possible  

---

### 10. Key Takeaways

- Integrate Jenkins with GitHub using Git plugin  
- Use Maven goals (`clean install`) for builds  
- Automate builds with webhooks  
- Use pipelines for scalable CI/CD  

---

### 11. Interview-Ready Summary

“To create a Jenkins job for a Maven project, I first ensure Git and Maven plugins are installed and tools are configured. Then I create a Freestyle or Pipeline job, connect it to the GitHub repository, and configure the build step using Maven goals like clean install. I also set up webhooks or polling for automatic triggers. Finally, I archive artifacts and follow best practices like using Jenkinsfile and secure credentials for maintainability and security.”

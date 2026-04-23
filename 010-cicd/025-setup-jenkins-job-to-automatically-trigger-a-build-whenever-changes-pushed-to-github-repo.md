### Question  
How would you set up a Jenkins job to automatically trigger a build whenever changes are pushed to a Git repository?

---

### 1. Overview

To automatically trigger builds on code changes, Jenkins integrates with Git repositories using:
- **Webhooks (recommended)**  
- **Polling (fallback option)**  

---

### 2. Create a New Jenkins Job

#### Steps:
- Open Jenkins  
- Click **New Item**  
- Choose:
  - **Freestyle Project** OR  
  - **Pipeline** (recommended for modern CI/CD)  
- Enter job name  
- Click **OK**

---

### 3. Configure Source Code Management (SCM)

#### Steps:
- Go to **Source Code Management → Git**  
- Enter:
  - Repository URL  
  - Credentials (if private repo)  
- Specify branch:
  ```
  main
  ```
  or
  ```
  develop
  ```

---

### 4. Configure Build Triggers

---

### 4.1 Option A: Webhook (Recommended)

#### Jenkins Configuration:
- Go to **Build Triggers**  
- Enable:
  ```
  GitHub hook trigger for GITScm polling
  ```

#### GitHub/GitLab Setup:
- Navigate to:
  ```
  Repository → Settings → Webhooks
  ```
- Add webhook URL:
  ```
  http://<jenkins-server>/github-webhook/
  ```
- Select:
  - Push events  

#### Result:
- Jenkins triggers build **immediately after code push**

---

### 4.2 Option B: Poll SCM (Fallback)

#### Jenkins Configuration:
- Enable:
  ```
  Poll SCM
  ```
- Add schedule:
  ```
  H/5 * * * *
  ```

#### Behavior:
- Jenkins checks repo every 5 minutes  
- Triggers build only if changes are detected  

---

### 5. Configure Build Steps

---

### 5.1 Freestyle Job

- Add:
  **Build → Execute shell**

```bash
mvn clean install
```

---

### 5.2 Pipeline Job

- Define steps in `Jenkinsfile`

---

### 6. Save and Test

#### Steps:
- Click **Save**  
- Push code to repository  

#### Expected Result:
- Jenkins automatically triggers build  

---

### 7. Best Practices

- Prefer **webhooks over polling** (faster and efficient)  
- Use **Jenkinsfile (Pipeline)** for better maintainability  
- Store credentials securely  
- Enable build notifications  

---

### 8. Key Takeaways

- Webhooks = real-time triggering  
- Poll SCM = periodic check fallback  
- Proper SCM configuration is essential  

---

### 9. Interview-Ready Summary

“To automatically trigger Jenkins builds on code changes, I configure the job with a Git repository and enable webhook-based triggers. I set up a webhook in GitHub pointing to the Jenkins endpoint, so whenever code is pushed, Jenkins immediately starts a build. As a fallback, I can use Poll SCM with a cron schedule, but webhooks are preferred because they are more efficient and provide real-time triggering.”

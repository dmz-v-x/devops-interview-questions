### Question  
What are the different ways to trigger Jenkins pipelines?

---

### 1. Overview

Jenkins pipelines can be triggered in multiple ways depending on the use case such as:
- Automation
- Scheduled builds
- Event-based triggers
- Manual execution  

These triggers are typically configured in the **“Build Triggers”** section of a Jenkins job.

---

### 2. Different Ways to Trigger Jenkins Pipelines

---

### 2.1 Poll SCM (Source Code Management Polling)

#### Description:
- Jenkins periodically checks the source code repository (e.g., Git) for changes.
- If changes are detected, it triggers a build automatically.

#### Configuration:
- Defined in **Build Triggers → Poll SCM**
- Uses cron-like syntax

#### Example:
```
H/5 * * * *
```
- Checks repository every 5 minutes

#### Key Points:
- Does NOT require external integration  
- Can increase load due to frequent polling  

---

### 2.2 Build Triggers (SCM Integration via Plugins)

#### Description:
- Jenkins integrates directly with SCM tools using plugins (e.g., Git plugin).
- Automatically triggers builds when changes are detected in a specific branch.

#### Configuration:
- Configure repository URL and branch in job settings  
- Enable trigger options in Build Triggers section  

#### Key Points:
- Easier integration with Git-based workflows  
- Works well with Jenkins-managed SCM configurations  

---

### 2.3 Webhooks (Event-Based Trigger - Recommended)

#### Description:
- Git platforms (GitHub, GitLab, Bitbucket) send an HTTP request (webhook) to Jenkins when code is pushed.

#### How It Works:
1. Developer pushes code  
2. GitHub sends webhook to Jenkins  
3. Jenkins triggers pipeline immediately  

#### Configuration:
- Enable **“GitHub hook trigger for GITScm polling”** in Jenkins  
- Add webhook URL in GitHub repository settings  

#### Key Points:
- Real-time trigger (no delay like polling)  
- Most efficient and widely used method  

---

### 3. Summary Comparison

| Method       | Trigger Type     | Real-Time | Load Impact | Use Case                          |
|--------------|-----------------|----------|------------|----------------------------------|
| Poll SCM     | Time-based      | No       | High       | Simple setups                    |
| Build Trigger| SCM-based       | Partial  | Medium     | Plugin-based automation          |
| Webhooks     | Event-based     | Yes      | Low        | Modern CI/CD pipelines (best)    |

---

### 4. Interview-Ready Summary

“Jenkins pipelines can be triggered in multiple ways such as Poll SCM, build triggers using SCM plugins, and webhooks. Poll SCM periodically checks for changes, while webhooks are event-based and trigger builds instantly when code is pushed. In modern CI/CD pipelines, webhooks are preferred because they are real-time and more efficient.”

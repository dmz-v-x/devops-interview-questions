### Question  
While running a job in Jenkins, the build failed. How will you resolve it?

---

### 1. Overview

A Jenkins build failure can be due to:
- Code issues  
- Configuration problems  
- Environment inconsistencies  
- Dependency or credential errors  

The key is to follow a **systematic debugging approach**.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Console Output

#### Action:
- Navigate:
  ```
  Jenkins UI → Job → Console Output
  ```

#### Look for:
- Error messages  
- Stack traces  
- Failed commands  

#### Examples:
- Maven build failure  
- Docker build error  
- Missing dependencies  

---

### 2.2 Verify Job Configuration

#### Check:
- Git repository URL  
- Branch existence  
- Build commands (Maven, Gradle, npm, etc.)  
- Tool versions:
  - JDK  
  - Node.js  
  - Python  

---

### 2.3 Check Build Environment

#### Verify Jenkins Agents:
- Agent is online  
- Required tools installed:
  - Maven  
  - Docker  
  - kubectl  

#### Workspace Issues:
```bash
rm -rf workspace/*
```

---

### 2.4 Check Credentials & Permissions

#### Common Issues:
- Incorrect Git credentials  
- Missing Docker/AWS/Azure credentials  
- Insufficient IAM permissions  

---

### 2.5 Check Dependencies

#### Possible Problems:
- Missing libraries (Maven/NPM/Pip)  
- Network/proxy issues blocking downloads  

---

### 2.6 Re-run the Build

#### Reason:
- Some failures are transient:
  - Network issues  
  - Registry downtime  

---

### 2.7 Isolate & Debug Locally

#### Steps:
- Clone repository locally  
- Run build command:
```bash
mvn clean install
```

#### Insight:
- If it fails locally → code issue  
- If it works locally → Jenkins/environment issue  

---

### 2.8 Check Jenkins Logs

#### Locations:
```bash
/var/log/jenkins/jenkins.log
```

#### Also check:
- Agent logs (node-specific issues)  

---

### 3. Key Takeaways

- Always start with console logs  
- Validate configuration and environment  
- Check credentials and dependencies  
- Reproduce locally to isolate issues  

---

### 4. Interview-Ready Summary

“If a Jenkins build fails, I first check the console output to identify the exact error. Then I verify the job configuration, including repository, branch, and build commands. I check the build environment and ensure all required tools and agents are properly configured. Next, I validate credentials and dependencies, and retry the build in case of transient issues. I also try to reproduce the issue locally to determine whether it’s a code problem or a Jenkins setup issue. This structured approach helps quickly identify and resolve the root cause.”

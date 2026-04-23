### Question  
You're experiencing sporadic failures in your Jenkins builds. How would you investigate and troubleshoot these failures?

---

### 1. Overview

Sporadic (intermittent) failures are usually caused by:
- Environment inconsistencies  
- Flaky tests  
- Resource issues  
- External dependencies  

The goal is to **identify patterns and isolate the root cause**.

---

### 2. Step-by-Step Troubleshooting Approach

---

### 2.1 Check Build Logs

#### Action:
- Go to:
  ```
  Jenkins → Job → Build # → Console Output
  ```

#### Look for:
- Error messages  
- Stack traces  
- Timeouts  
- Dependency failures  

---

### 2.2 Compare Successful vs Failed Builds

#### Action:
- Compare logs of:
  - Passing builds  
  - Failing builds  

#### Identify patterns:
- Specific nodes  
- Time of execution  
- Branch-specific failures  

---

### 2.3 Verify Build Environment

#### Check Jenkins Agents:

- Disk space  
- Memory/CPU usage  
- Installed tools (Java, Maven, Node, etc.)  

#### Ensure:
- Same OS and tool versions across nodes  
- No environment drift  

---

### 2.4 Check for Flaky Tests

#### Common Causes:
- Timing issues  
- External dependencies  
- Race conditions  

#### Actions:
- Run tests multiple times locally  
- Mock external services  
- Add retry logic for unstable tests  

---

### 2.5 Check SCM and Dependencies

#### Verify:
- Git commit differences  
- Dependency updates  

#### Best Practice:
- Use **version pinning** to avoid unexpected changes  

---

### 2.6 Inspect Jenkins Configuration

#### Check:
- Parallel builds causing conflicts  
- Shared resources (files, ports, DB)  
- Global environment variables  
- Credentials consistency  

---

### 2.7 Enable Debugging

#### Increase verbosity:

```bash
mvn -X
```

#### Add diagnostic commands:

```bash
env
docker ps
```

#### Benefits:
- More visibility into failures  
- Helps isolate issues  

---

### 2.8 Stabilize the Pipeline

#### After identifying root cause:

- Fix flaky tests  
- Standardize environments (Docker, containers)  
- Add retry mechanism  

#### Example (Retry in Jenkins Pipeline):

```groovy
retry(3) {
    sh 'mvn test'
}
```

---

### 3. Additional Best Practices

- Use containerized builds for consistency  
- Monitor system metrics (CPU, memory, disk)  
- Use alerts for failures  
- Maintain clean workspace  

---

### 4. Key Takeaways

- Always start with logs  
- Look for patterns across builds  
- Environment consistency is critical  
- Flaky tests are a common root cause  

---

### 5. Interview-Ready Summary

“To troubleshoot sporadic Jenkins build failures, I start by analyzing console logs and comparing failed and successful builds to identify patterns. I then verify the build environment across agents to ensure consistency and check for flaky tests, which are a common cause of intermittent failures. I also review SCM changes and dependencies, inspect Jenkins configuration for issues like parallel conflicts, and enable verbose logging for deeper insights. Once the root cause is identified, I stabilize the pipeline by fixing tests, standardizing environments using containers, and adding retry mechanisms for transient failures.”

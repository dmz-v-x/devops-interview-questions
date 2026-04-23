### Question  
Your Jenkins server is running low on disk space. How would you address this issue?

---

### 1. Overview

Low disk space in Jenkins can lead to:
- Build failures  
- Inability to write logs/artifacts  
- System instability  

The solution is a combination of **cleanup, optimization, and monitoring**.

---

### 2. Step-by-Step Resolution

---

### 2.1 Clean Up Old Builds

#### Action:
- Remove unnecessary build history  

#### Configure in Jenkins:
- Go to:
  ```
  Job → Configure → Build Discarder
  ```

- Set:
  - Max number of builds  
  - Max days to keep builds  

#### Pipeline Example:
```groovy
properties([
  buildDiscarder(logRotator(numToKeepStr: '10', daysToKeepStr: '30'))
])
```

---

### 2.2 Remove Unused Workspaces

#### Problem:
- Old or unused job workspaces consume large space  

#### Manual Cleanup:
```bash
rm -rf /var/lib/jenkins/workspace/old_job_name
```

#### Better Approach:
- Use **Workspace Cleanup Plugin**  

---

### 2.3 Clean Cache and Temporary Files

```bash
rm -rf /var/lib/jenkins/cache/*
rm -rf /var/lib/jenkins/tmp/*
```

#### Purpose:
- Remove unused cached data  
- Free temporary storage  

---

### 2.4 Clean Docker Resources (If Used)

#### Problem:
- Docker images, containers, and volumes accumulate  

#### Cleanup Commands:
```bash
docker system prune -af
docker volume prune -f
```

---

### 2.5 Manage Logs

#### Check log size:
```bash
du -sh /var/log/jenkins
```

#### Rotate logs:
```bash
logrotate /etc/logrotate.d/jenkins
```

#### Purpose:
- Prevent logs from growing indefinitely  

---

### 2.6 Move JENKINS_HOME to Larger Disk (Optional)

#### When Needed:
- If cleanup is not sufficient  

#### Steps:
- Move data to a larger disk  
- Update Jenkins configuration:
  ```
  /etc/default/jenkins
  ```

---

### 2.7 Monitor Disk Usage

#### Actions:
- Use monitoring tools  
- Set alerts for disk thresholds  

#### Tools:
- Prometheus + Grafana  
- Cloud monitoring services  

---

### 3. Additional Best Practices

- Archive artifacts externally (S3, Nexus, Artifactory)  
- Clean workspaces after builds  
- Use ephemeral agents (containers)  
- Avoid storing unnecessary data in JENKINS_HOME  

---

### 4. Key Takeaways

- Clean builds, workspaces, and logs regularly  
- Use automation for cleanup  
- Monitor proactively  

---

### 5. Interview-Ready Summary

“To resolve low disk space issues in Jenkins, I first clean up old builds by configuring build retention policies. Then I remove unused workspaces and clear cache and temporary files. If Docker is used, I prune unused images and containers. I also manage logs using log rotation and, if needed, move JENKINS_HOME to a larger disk. Finally, I set up monitoring and alerts to proactively manage disk usage and prevent future issues.”

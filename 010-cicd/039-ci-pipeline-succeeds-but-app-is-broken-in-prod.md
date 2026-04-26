### Question  
CI Pipeline Succeeds but App is Broken in Prod — What Action Will You Take?

---

### Answer  

If the CI/CD pipeline passes but the application breaks in production, it usually indicates gaps in validation, environment mismatches, or runtime issues not caught during testing.

---

### Step-by-Step Troubleshooting Approach

---

### 1. Initiate Incident Response

- Notify:
  - Team and stakeholders  

- Actions:
  - Document the issue  
  - Assess severity  

- If critical:
  - Trigger rollback  
  - Redeploy last stable version  

---

### 2. Check Production Logs and Monitoring

- Use:
  - ELK  
  - CloudWatch  
  - Observability tools  

- Inspect:

  - HTTP status codes:
    - 5xx errors  
    - 4xx errors  

  - Application logs  
  - Metrics:
    - CPU  
    - Memory  
    - Database errors  
    - Timeouts  

---

### 3. Compare Staging vs Production

Check for differences:

- Environment variables  
- Backend services  
- Feature flags  

Also verify:

- Artifact deployed in production is the same one tested in staging  

---

### 4. Check Secrets and External Integrations

Validate:

- API keys  
- Database credentials  
- Third-party integrations  

Common issues:

- Expired or rotated credentials  
- Missing secrets  

---

### 5. Check Infrastructure Differences

Look for differences in:

- Kubernetes namespaces  
- Load balancer configurations  
- Terraform state  
- AMIs or instance configurations  
- Security groups  

---

### Immediate Actions

- Rollback:
  - Using Git tags  
  - Helm chart versions  
  - AMI snapshots  

- Create:
  - Incident report  
  - Postmortem  

- Assign:
  - Root Cause Analysis (RCA)  

- Apply:
  - Hotfix only after RCA  

---

### Preventive Measures

- Add:
  - Automated smoke tests post-deployment  

- Use:
  - Canary deployments  
  - Blue-green deployments  

- Ensure:
  - Staging and production parity  

- Validate:
  - Secrets and configurations before deploy  

- Enable:
  - Real-time alerts for anomalies  

---

### Key Takeaways

- CI success does not guarantee:
  - Production success  

- Root causes are often:
  - Environment differences  
  - Missing configs  
  - External dependency failures  

---

### Interview-Ready Summary

“If a CI pipeline succeeds but the app breaks in production, I first initiate incident response and, if needed, roll back to the last stable version. Then I check production logs and monitoring to identify errors, compare staging and production environments for differences, and verify secrets and external integrations. I also check infrastructure differences like Kubernetes configs or load balancers. After resolving the issue, I conduct an RCA and implement preventive measures like smoke tests, canary deployments, and ensuring environment parity to avoid similar issues in the future.”

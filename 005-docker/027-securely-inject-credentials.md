### Question  
How do you securely inject credentials into a CI/CD pipeline?

---

### Answer  

### 1. Never Hardcode Secrets  

- Do NOT store:
  - API keys  
  - passwords  
  - tokens  

in:

- Source code  
- Dockerfiles  
- Config files  

---

### 2. Use a Secret Manager (Best Practice)  

Store secrets in dedicated systems:

- HashiCorp Vault  
- AWS Secrets Manager  
- Azure Key Vault  
- GCP Secret Manager  

---

#### Flow  

    CI/CD Pipeline → Fetch Secret → Use at Runtime

---

### 3. Use CI/CD Built-in Secret Stores  

Most platforms provide encrypted secret storage:

- GitHub Actions → Secrets  
- GitLab CI → Variables  
- Jenkins → Credentials  
- Azure DevOps → Secure variables  

---

#### Example (GitHub Actions)  

    env:
      DB_PASSWORD: ${{ secrets.DB_PASSWORD }}

---

### 4. Apply Least Privilege (RBAC)  

- Only allow required jobs to access secrets  
- Use role-based access control  

---

#### Example  

- Build job → no DB access  
- Deploy job → limited DB access  

---

### 5. Mask Secrets in Logs  

- Ensure secrets are hidden in logs  

Example:

    ****** instead of actual value  

---

### 6. Use Short-Lived Credentials  

Avoid long-lived credentials.

---

#### Use  

- OIDC tokens  
- Temporary IAM roles  
- Vault dynamic secrets  

---

Benefits:

- Reduced risk if leaked  

---

### 7. Rotate Secrets Regularly  

- Periodically update:
  - API keys  
  - tokens  
  - passwords  

---

### 8. Inject at Runtime (Not Build Time)  

- Prefer:

    docker run -e DB_PASSWORD=...

- Avoid:

    ARG / ENV in Dockerfile for secrets  

---

### 9. Use Environment Variables or Files  

---

#### Environment Variables  

    export API_KEY=...

---

#### Mounted Secrets (Better)  

    /run/secrets/db_password

---

### 10. Key Security Principles  

---

- Least privilege  
- No hardcoding  
- Runtime injection  
- Short-lived access  

---

### 11. Tricky Interview Questions  

---

Why not store secrets in Docker image?  

- Anyone with image can extract them  

---

What is OIDC in CI/CD?  

- Secure token-based authentication without storing secrets  

---

Are environment variables secure?  

- Better than hardcoding, but still need protection  

---

Best place to store secrets?  

- External secret manager  

---

### Interview Summary  

“To securely inject credentials into a CI/CD pipeline, I use secret managers or the CI/CD platform’s encrypted secret store. I follow least privilege access, ensure secrets are masked in logs, and prefer short-lived tokens. Secrets are injected at runtime rather than hardcoded, ensuring both security and compliance.”

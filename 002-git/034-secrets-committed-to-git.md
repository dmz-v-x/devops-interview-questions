### Question  
A teammate accidentally committed a Kubernetes Secret (base64 encoded) to Git. What should you do?

---

### Answer  

This is a **security incident**. Base64 is **not encryption**, so the secret must be treated as **compromised immediately**.

---

### 1. Step 1: Rotate the Compromised Secret (Most Critical)

- Assume the secret is exposed  

---

#### Actions:

- Generate a new secret:
  - New password / API key / token  

---

#### Update Kubernetes Secret:

```bash
kubectl create secret generic my-secret \
  --from-literal=password=newpassword \
  --dry-run=client -o yaml | kubectl apply -f -
```

---

#### Then:

- Restart or update workloads using the secret  
- Ensure no service uses the old value  

---

### 2. Step 2: Remove Secret from Git History

---

#### If only in latest commit:

```bash
git reset HEAD~1
git restore --staged secret.yaml
rm secret.yaml
git commit -m "Remove secret from repo"
```

---

#### If already pushed (full cleanup required):

Use **BFG Repo-Cleaner** or `git filter-repo`:

```bash
bfg --delete-files secret.yaml
```

---

#### Then force push:

```bash
git push --force
```

---

#### Important:

- Inform team before force push  
- Everyone must re-clone or reset  

---

### 3. Step 3: Prevent Future Incidents

---

#### Add to `.gitignore`:

```
secrets.yaml
*.key
```

---

#### Use Security Tools:

- `git-secrets`  
- `pre-commit hooks`  
- Secret scanners (TruffleHog, Gitleaks)  

---

#### Best Practices:

- Never store secrets in Git  
- Use:
  - Kubernetes Sealed Secrets  
  - External secret managers:
    - AWS Secrets Manager  
    - HashiCorp Vault  

---

### 4. Key Lessons

- Base64 ≠ encryption  
- Secrets in Git = major risk  
- Always:
  - Rotate  
  - Remove  
  - Prevent  

---

### 5. Impact Awareness

- Even private repos can be exposed  
- Attackers scan Git history  
- Old commits remain accessible unless cleaned  

---

### 6. Interview-Ready Summary

“If a Kubernetes Secret is committed to Git, I treat it as compromised immediately. First, I rotate the secret and update all dependent services. Then I remove the secret from the Git history using tools like BFG or git filter-repo and force push the cleaned history. Finally, I implement preventive measures like .gitignore rules, pre-commit hooks, and secret management solutions such as Vault or Sealed Secrets to avoid future incidents.”

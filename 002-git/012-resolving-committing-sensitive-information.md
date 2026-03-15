### Question
You accidentally committed sensitive information such as API keys or passwords to a Git repository. How would you handle this situation?

### Answer

If sensitive information such as API keys, passwords, or tokens is accidentally committed to a Git repository, it must be handled immediately because Git stores all commit history. Simply deleting the file and committing again does **not remove the sensitive data from previous commits**.

The correct approach involves removing the secret from the repository history, updating the credentials, and implementing safeguards to prevent it from happening again.

---

### Step 1: Remove the Sensitive Data from Git History

Since Git keeps a complete history of commits, the secret must be removed from the entire history.

#### Option 1: Using `git filter-repo` (Recommended Modern Approach)

    git filter-repo --path path/to/secret-file --invert-paths

Explanation:

- This command removes the specified file from all commits in the repository history.
- `git-filter-repo` is a modern and faster tool for rewriting Git history.

If the tool is not installed, it must be installed first.

---

#### Option 2: Using `git filter-branch` (Older Method)

    git filter-branch --force --index-filter \
    "git rm --cached --ignore-unmatch path/to/secret-file" \
    --prune-empty --tag-name-filter cat -- --all

Explanation:

- This removes the file from the entire commit history.
- This command rewrites all commits that contained the sensitive file.

Although still functional, this method is slower and generally replaced by `git filter-repo`.

---

### Step 2: Force Push the Cleaned Repository

After rewriting the repository history, the cleaned version must be pushed to the remote repository.

    git push origin --force --all
    git push origin --force --tags

Important note:

- Force pushing rewrites the remote repository history.
- Other developers working on the repository will need to **re-clone or reset their local repositories**.

---

### Step 3: Rotate the Compromised Credentials

Even if the secret is removed from the repository, it should be considered compromised.

Immediately take the following actions:

- Revoke the exposed API keys or tokens
- Generate new credentials
- Update the application with the new credentials

Secrets should then be stored securely using methods such as:

- environment variables
- secret management systems
- cloud secrets managers

---

### Step 4: Prevent Future Accidents

To avoid committing secrets in the future, several preventive measures should be implemented.

Common practices include:

Add sensitive files to `.gitignore` so they cannot be committed accidentally.

Use tools such as:

- `git-secrets`
- `pre-commit` hooks

These tools scan commits and block commits containing potential secrets.

Store sensitive information outside the repository using secure systems such as:

- HashiCorp Vault
- AWS Secrets Manager
- Kubernetes Secrets

These systems manage secrets securely without exposing them in code repositories.

---

### Interview Summary

If sensitive data is accidentally committed to a Git repository, I would remove the secret from the repository history using tools like `git filter-repo`, force push the cleaned repository, immediately rotate the compromised credentials, and implement preventive controls such as `.gitignore`, pre-commit secret scanning tools, and secure secret management systems to avoid similar incidents in the future.

### Question
How would you secure sensitive configuration files on a Linux server?

### Answer

Sensitive configuration files on Linux systems often contain **passwords, API keys, certificates, database credentials, and application secrets**. If these files are exposed or improperly secured, they can lead to **unauthorized access, data breaches, and system compromise**.

Securing configuration files involves using proper **file permissions, encryption, access controls, monitoring, and secret management practices**.

---

### Why Secure Configuration Files?

Sensitive configuration files may contain critical information such as:

- Passwords and API keys  
  Example: `/etc/mysql/my.cnf`, `/etc/ssh/sshd_config`

- Application secrets  
  Example: `.env` files or `/var/lib/jenkins/credentials.xml`

- Network credentials or SSL/TLS certificates

If these files are exposed, attackers may gain **privileged system access, database access, or application control**.

---

### File Permissions and Ownership

Proper file permissions ensure that only authorized users or services can read or modify configuration files.

---

#### Check File Permissions

Use the following command to view permissions:

```
ls -l /path/to/config/file
```

Example permission format:

```
-rwxr-xr-x
```

This represents permissions for:

- owner
- group
- others

---

#### Restrict Access

Sensitive files should normally be accessible **only to the owner**, usually `root` or the application user.

Example:

```
sudo chown root:root /etc/myapp/config.conf
sudo chmod 600 /etc/myapp/config.conf
```

Explanation:

- `chmod 600` → owner can **read and write**, group and others have **no access**
- `chmod 640` → owner **read/write**, group **read**, others **no access**

These restrictions prevent unauthorized users from accessing sensitive configuration data.

---

### Use Encryption

Encryption protects configuration files even if someone gains access to them.

---

#### Encrypt Using GPG

Encrypt a file with a password:

```
gpg -c /etc/myapp/config.conf
```

Decrypt the encrypted file:

```
gpg /etc/myapp/config.conf.gpg
```

---

#### Encrypt Using OpenSSL

Encryption example:

```
openssl enc -aes-256-cbc -salt -in config.conf -out config.conf.enc
```

Decrypt the file:

```
openssl enc -aes-256-cbc -d -in config.conf.enc -out config.conf
```

---

#### Use Environment Variables for Secrets

Instead of storing credentials directly in configuration files, store them in **environment variables**, which reduces the risk of exposing secrets in files.

---

### Limit Access Using SELinux or AppArmor

Mandatory access control systems provide additional security beyond basic file permissions.

---

#### SELinux

SELinux enforces security policies that restrict which processes can access specific files.

Check the SELinux context:

```
ls -Z /etc/myapp/config.conf
```

Change the SELinux context:

```
chcon -t etc_t /etc/myapp/config.conf
```

---

#### AppArmor

AppArmor confines applications so they can only access allowed files and directories.

This helps prevent compromised applications from accessing sensitive configuration files.

---

### Version Control Safety

Sensitive configuration files should **never be committed to version control systems**.

Add them to `.gitignore`:

```
.env
config/secrets.yml
```

Use dedicated **secret management tools** instead of storing secrets in repositories:

- HashiCorp Vault
- AWS Secrets Manager
- Kubernetes Secrets

These tools provide centralized, secure storage for credentials.

---

### Backup Security

Configuration backups should also be protected using encryption.

Example encrypted backup:

```
tar czf - /etc/myapp | gpg -c -o /backup/myapp_config_backup.tar.gz.gpg
```

This ensures that even if backup files are accessed, the configuration data remains protected.

---

### Monitor Access

Monitoring access to configuration files helps detect unauthorized activity.

Use the Linux auditing system `auditd`.

Monitor file access:

```
sudo auditctl -w /etc/myapp/config.conf -p rwa -k config_watch
```

Search audit logs:

```
ausearch -f /etc/myapp/config.conf
```

This allows administrators to track who accessed or modified sensitive files.

---

### Tricky Interview Questions

How would you protect files like `/etc/shadow` or `/etc/passwd`?

Use strict permissions such as:

```
chmod 600 /etc/shadow
```

Also enforce additional security controls using **SELinux or AppArmor**, and never store copies unencrypted.

---

How should secrets be stored for applications running on multiple servers?

Use centralized secret management tools such as:

- HashiCorp Vault
- Cloud-based secret managers (AWS Secrets Manager)
- Kubernetes Secrets

---

How can accidental commits of secrets be prevented?

- Use `.gitignore` to exclude sensitive files
- Use tools like **git-secrets** or **pre-commit hooks** to detect credentials before committing

---

What is the difference between file permissions and encryption?

- **File permissions** control **who can access a file**
- **Encryption** ensures that even if someone accesses the file, the **data remains unreadable**

---

### Interview Summary

To secure sensitive configuration files on Linux, administrators should enforce strict file permissions, use encryption, apply access control policies like SELinux or AppArmor, avoid storing secrets in version control, secure backups, and monitor access using auditing tools.

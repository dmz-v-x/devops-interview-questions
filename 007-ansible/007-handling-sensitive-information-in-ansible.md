### Question
How do you handle Sensitive Information in Ansible

### 1. Handling Sensitive Information in Ansible

Sensitive data like passwords, API keys, and credentials must **never be stored in plain text** in playbooks or repositories. Ansible provides **Ansible Vault** to securely encrypt and manage such data.

---

### 1.1 Install and Verify Ansible Vault

Ansible Vault comes bundled with Ansible.

Check installation:

    ansible --version

If Ansible is installed, Vault is already available.

---

### 1.2 Create an Encrypted File

Create a new encrypted file:

    ansible-vault create secrets.yml

You will be prompted to set a **vault password**.

Then add sensitive data:

    db_user: admin
    db_password: MySecretPassword123
    api_key: 12345-ABCDE

Save and exit.

Now the file is **fully encrypted** and unreadable without the password.

---

### 1.3 Edit an Encrypted File

To modify the encrypted file later:

    ansible-vault edit secrets.yml

This decrypts temporarily, allows editing, and encrypts again on save.

---

### 1.4 Use Encrypted Variables in Playbooks

Include the encrypted file using `vars_files`.

Example playbook:

    - hosts: webservers
      become: yes
      vars_files:
        - secrets.yml

      tasks:
        - name: Print database user (for demo)
          debug:
            msg: "DB User is {{ db_user }}"

        - name: Use DB password
          shell: "echo {{ db_password }} > /tmp/db_pass.txt"

At runtime, Ansible decrypts the file automatically.

---

### 1.5 Run the Playbook

Provide vault password during execution:

    ansible-playbook site.yml --ask-vault-pass

OR use a password file (for automation):

    ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt

---

### 1.6 Encrypt Existing Files

If secrets already exist in plain text:

    ansible-vault encrypt vars.yml

To decrypt:

    ansible-vault decrypt vars.yml

---

### 1.7 Change Vault Password (Re-key)

    ansible-vault rekey secrets.yml

---

### 1.8 Best Practices

- Never commit plain-text secrets to Git  
- Always separate secrets using `vars_files`  
- Use vault password files in CI/CD securely  
- Restrict access to vault passwords  
- Prefer centralized secret managers (Vault, AWS Secrets Manager, etc.)  

---

### Final Summary

Ansible Vault ensures:
- Encryption of sensitive data  
- Secure usage in playbooks  
- Safe automation without exposing secrets  

---

---

### 2. Setting Up NGINX Reverse Proxy for App Running on Port 3000

A reverse proxy allows NGINX to forward client requests to a backend application (e.g., Node.js on port 3000).

---

### 2.1 Install NGINX

On Ubuntu/Debian:

    sudo apt update
    sudo apt install nginx -y

---

### 2.2 Create NGINX Configuration File

Create a new config:

    sudo nano /etc/nginx/sites-available/myapp

Add configuration:

    server {
        listen 80;
        server_name myapp.example.com;   # replace with domain or IP

        location / {
            proxy_pass http://127.0.0.1:3000;

            # Preserve client information
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

---

### 2.3 Enable the Site

    sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled/

---

### 2.4 Test Configuration

    sudo nginx -t

If successful:

    sudo systemctl reload nginx

---

### 2.5 Configure Firewall

Allow HTTP/HTTPS:

    sudo ufw allow 'Nginx Full'

---

### 2.6 Verify Setup

Open in browser:

    http://myapp.example.com

Requests will be forwarded to:

    http://127.0.0.1:3000

---

### 2.7 Best Practices

- Enable HTTPS using Let’s Encrypt (certbot)  
- Use gzip compression for performance  
- Configure caching where needed  
- Run backend app with systemd or process manager (PM2)  
- Monitor logs in `/var/log/nginx/`  

---

### Final Summary

- NGINX acts as a **reverse proxy** between users and backend apps  
- It improves **security, scalability, and performance**  
- Combined with SSL and monitoring, it becomes production-ready  

### Question
Configure NGINX as a Reverse Proxy Using Ansible

### 1. Configure NGINX as a Reverse Proxy Using Ansible

We can automate reverse proxy setup using Ansible by creating a playbook that:

- Installs NGINX  
- Deploys reverse proxy configuration  
- Enables and reloads NGINX  
- Ensures the service is running  

---

### 1.1 Complete Ansible Playbook

```yaml
---
- name: Configure Nginx as a Reverse Proxy
  hosts: webservers
  become: yes

  tasks:
    - name: Install Nginx (Debian/Ubuntu)
      apt:
        name: nginx
        state: present
        update_cache: yes
      when: ansible_os_family == "Debian"

    - name: Install Nginx (RHEL/CentOS)
      yum:
        name: nginx
        state: present
      when: ansible_os_family == "RedHat"

    - name: Configure Nginx reverse proxy
      template:
        src: reverse-proxy.conf.j2
        dest: /etc/nginx/sites-available/reverse-proxy.conf
      notify:
        - Reload Nginx

    - name: Enable reverse proxy site (Debian-based)
      file:
        src: /etc/nginx/sites-available/reverse-proxy.conf
        dest: /etc/nginx/sites-enabled/reverse-proxy.conf
        state: link
      when: ansible_os_family == "Debian"

    - name: Ensure Nginx is running and enabled
      service:
        name: nginx
        state: started
        enabled: yes

  handlers:
    - name: Reload Nginx
      service:
        name: nginx
        state: reloaded
```

---

### 1.2 Jinja2 Template (reverse-proxy.conf.j2)

```nginx
server {
    listen 80;

    server_name myapp.example.com;

    location / {
        proxy_pass http://127.0.0.1:5000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

### 1.3 How It Works (Step-by-Step)

1. Installs NGINX depending on OS family (Debian or RedHat)  
2. Deploys reverse proxy configuration using a template  
3. Enables the site (for Debian-based systems)  
4. Triggers handler only if configuration changes  
5. Ensures NGINX is running and enabled at boot  

---

### 1.4 Key Concepts Used

- Idempotency → Safe to run multiple times  
- Template module → Dynamic configuration  
- Handlers → Restart/reload only when needed  
- Conditionals (when) → OS-specific logic  

---

### 1.5 Best Practices

- Use roles (`roles/nginx`) for better structure  
- Parameterize values (port, domain) using variables  
- Use handlers instead of always restarting services  
- Validate config before reload (`nginx -t`)  

---

---

### 2. Ansible Playbook to Install NGINX

---

### 2.1 Playbook: install_nginx.yaml

```yaml
---
- name: Install and configure NGINX
  hosts: webservers
  become: yes

  tasks:
    - name: Update package cache (Debian/Ubuntu)
      apt:
        update_cache: yes
      when: ansible_os_family == "Debian"

    - name: Install NGINX on Debian/Ubuntu
      apt:
        name: nginx
        state: present
      when: ansible_os_family == "Debian"

    - name: Install NGINX on RedHat/CentOS
      yum:
        name: nginx
        state: present
      when: ansible_os_family == "RedHat"

    - name: Ensure NGINX is running and enabled
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### 2.2 How It Works

- Runs on `webservers` inventory group  
- Detects OS using `ansible_os_family`  
- Uses:
  - `apt` for Debian/Ubuntu  
  - `yum` for RHEL/CentOS  
- Installs NGINX package  
- Starts and enables service  

---

### 2.3 Key Concepts

- Cross-platform support using conditionals  
- Service management via Ansible  
- Automation of package installation  

---

### 2.4 Best Practices (Interview Points)

- Use roles for reusable nginx setup  
- Use handlers for restart/reload after config change  
- Maintain idempotency (safe repeated runs)  
- Separate configs using templates and variables  

---

### Final Summary

- Reverse proxy setup = Install + Configure + Enable + Reload  
- Ansible ensures automation, consistency, and repeatability  
- Using templates + handlers makes configuration dynamic and efficient  

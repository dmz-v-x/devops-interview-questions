### Question  
How do you install Nginx using Ansible?

---

### Short Explanation of the Question  

This question checks your ability to write a basic Ansible playbook to install and manage a service on target machines.

---

### Answer  

You can install Nginx using Ansible by using the appropriate package module (apt for Debian/Ubuntu or yum/dnf for RHEL-based systems) and then ensuring the service is started and enabled.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### Example Playbook (Ubuntu/Debian)

```yaml
- name: Install and start Nginx on Ubuntu
  hosts: webservers
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start and enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### Example Playbook (RHEL/CentOS)

```yaml
- name: Install and start Nginx on RHEL
  hosts: webservers
  become: yes

  tasks:
    - name: Install Nginx
      yum:
        name: nginx
        state: present

    - name: Start and enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### OS-Agnostic Playbook (Best Practice)

```yaml
- name: Install and start Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install Nginx
      package:
        name: nginx
        state: present

    - name: Start and enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### Optional: Open Firewall (RHEL)

```yaml
- name: Allow HTTP traffic
  firewalld:
    service: http
    state: enabled
    permanent: yes
    immediate: yes
```

---

### Key Concepts Used  

- package / apt / yum → install software  
- service → manage service state  
- become: yes → run with sudo privileges  

---

### Real-World Tip  

- Use package module for cross-platform compatibility  
- Combine with roles for reusable web server setup  

---

### Interview-Ready Summary  

“To install Nginx using Ansible, I use the package module to install it and the service module to start and enable it. For cross-platform compatibility, I prefer the package module instead of OS-specific modules like apt or yum.”

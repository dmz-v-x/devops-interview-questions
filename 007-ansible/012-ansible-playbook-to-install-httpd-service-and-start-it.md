### Question  
Can you write an Ansible playbook to install httpd service and get it running? (Optionally also configure firewall)

---

### Short Explanation of the Question  

This question tests your practical knowledge of Ansible—specifically writing a playbook to install a package, manage services, and optionally configure firewall rules.

---

### Answer  

Yes, we can write an Ansible playbook that installs the httpd (Apache) service, starts and enables it, and optionally allows HTTP traffic through the firewall.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### Basic Ansible Playbook (Install + Start httpd)

```yaml
- name: Install and start Apache (httpd)
  hosts: webservers
  become: yes

  tasks:
    - name: Install httpd package
      yum:
        name: httpd
        state: present

    - name: Start httpd service
      service:
        name: httpd
        state: started
        enabled: yes
```

---

### Explanation  

- hosts: webservers → runs on target group  
- become: yes → uses sudo privileges  
- yum → installs package (for RHEL/CentOS)  
- service → ensures service is running and enabled on boot  

---

### Optional: Configure Firewall (firewalld)

```yaml
- name: Allow HTTP through firewall
  firewalld:
    service: http
    permanent: yes
    state: enabled
    immediate: yes
```

---

### Full Playbook (With Firewall)

```yaml
- name: Install, start Apache and configure firewall
  hosts: webservers
  become: yes

  tasks:
    - name: Install httpd package
      yum:
        name: httpd
        state: present

    - name: Start and enable httpd
      service:
        name: httpd
        state: started
        enabled: yes

    - name: Allow HTTP in firewall
      firewalld:
        service: http
        permanent: yes
        state: enabled
        immediate: yes
      when: ansible_facts['os_family'] == "RedHat"
```

---

### Notes  

- Uses yum → works on RHEL/CentOS/Amazon Linux  
- For Ubuntu/Debian, replace yum with apt and httpd with apache2  
- firewalld must be installed and running  

---

### Interview-Ready Summary  

“Yes, I can write an Ansible playbook to install and run httpd by using the yum module to install the package and the service module to start and enable it. Optionally, I can configure the firewall using the firewalld module to allow HTTP traffic. This ensures the web server is installed, running, and accessible.”

### Question
Explain ways to run the same Ansible playbook on different nodes with different ports and usernames.

### Answer

In Ansible, you can run the **same playbook across multiple hosts** while using **different SSH usernames and ports per host**. This is handled through inventory variables, host/group variables, or runtime overrides.

---

### 1. Using Inventory with Host-Specific Variables

#### Purpose
Define connection details (IP, username, port) directly in the inventory file.

#### Example: `hosts.ini`

```
[webservers]
web1 ansible_host=192.168.1.10 ansible_user=admin ansible_port=2222
web2 ansible_host=192.168.1.11 ansible_user=root ansible_port=2200
```

#### Explanation

- `ansible_host` → target IP/hostname  
- `ansible_user` → SSH username  
- `ansible_port` → SSH port  

#### Run Playbook

```
ansible-playbook -i hosts.ini site.yml
```

#### Key Points

- Each host uses its own connection settings  
- Simple and effective for small setups  

---

### 2. Using `host_vars/` (Host-Specific Configuration)

#### Purpose
Store variables per host in separate YAML files for better organization.

#### Directory Structure

```
host_vars/
  web1.yml
  web2.yml
```

#### Example: `host_vars/web1.yml`

```
ansible_user: admin
ansible_port: 2222
```

#### Example: `host_vars/web2.yml`

```
ansible_user: root
ansible_port: 2200
```

#### Key Points

- Automatically picked by Ansible  
- Scalable and clean for large environments  
- Keeps inventory file simple  

---

### 3. Using `group_vars/` (Group-Level Configuration)

#### Purpose
Define shared connection settings for a group of hosts.

#### Example: `group_vars/webservers.yml`

```
ansible_user: admin
ansible_port: 2222
```

#### Key Points

- Applies to all hosts in `[webservers]`  
- Reduces duplication  
- Useful when many hosts share the same configuration  

---

### 4. Passing Extra Variables via CLI

#### Purpose
Temporarily override connection settings during execution.

#### Command

```
ansible-playbook -i hosts.ini site.yml \
  -e "ansible_user=customuser ansible_port=2223"
```

#### Key Points

- Overrides inventory and variable files  
- Useful for testing or temporary changes  
- Does not modify configuration files  

---

### 5. Example Playbook

```
- hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present
```

#### Key Points

- Same playbook runs on all hosts  
- Connection details are dynamically picked from:
  - inventory  
  - host_vars  
  - group_vars  
  - extra vars  

---

### 6. Summary Table

| Method | Use Case | Notes |
|---|---|---|
| Inventory host vars | Different users/ports per host | Simple, quick setup |
| `host_vars/` | Large-scale host-specific configs | Clean and scalable |
| `group_vars/` | Shared config for multiple hosts | Avoids repetition |
| Extra vars (`-e`) | Temporary override | One-time execution |

---

### Final Summary

You can run the same Ansible playbook across multiple hosts with different usernames and ports by defining connection variables in **inventory, host_vars, group_vars, or via CLI overrides**. This flexibility allows centralized automation while maintaining host-specific configurations.

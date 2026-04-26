### Question  
What are different types of variables (vars) in Ansible?

---

### Short Explanation of the Question  

This question tests your understanding of how variables are defined, scoped, and used in Ansible across different levels.

---

### Answer  

Ansible supports multiple types of variables based on where and how they are defined. These include playbook variables, inventory variables, role variables, facts, registered variables, and more. Each type has a different scope and precedence.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

## 1. Playbook Variables  

Defined inside a playbook.

```yaml
- hosts: all
  vars:
    app_port: 8080
```

---

## 2. Inventory Variables  

Defined in inventory files.

---

### Host Variables  

```ini
web1 ansible_host=192.168.1.10 app_port=8080
```

---

### Group Variables  

```ini
[webservers:vars]
app_port=8080
```

---

## 3. Host Vars & Group Vars Files  

Stored in directory structure:

```text
group_vars/
  webservers.yml

host_vars/
  web1.yml
```

---

## 4. Role Variables  

---

### Defaults (Lowest Priority)  

```yaml
# roles/web/defaults/main.yml
app_port: 80
```

---

### Vars (Higher Priority)  

```yaml
# roles/web/vars/main.yml
app_port: 8080
```

---

## 5. Facts (System Variables)  

- Automatically gathered  

```yaml
ansible_os_family
ansible_hostname
```

---

## 6. Registered Variables  

- Capture task output  

```yaml
- name: Run command
  command: uptime
  register: result
```

---

## 7. set_fact Variables  

- Create variables dynamically  

```yaml
- set_fact:
    version: "1.0"
```

---

## 8. Extra Variables (Highest Priority)  

- Passed via CLI  

```bash
ansible-playbook play.yml -e "app_port=9090"
```

---

## 9. Environment Variables  

- Pulled from system  

```yaml
db_password: "{{ lookup('env', 'DB_PASSWORD') }}"
```

---

## 10. Prompt Variables  

- Ask user input at runtime  

```yaml
vars_prompt:
  - name: username
    prompt: "Enter username"
```

---

## Summary Table  

| Type              | Description                          |
|------------------|--------------------------------------|
| Playbook vars     | Defined in playbook                  |
| Inventory vars    | Defined in inventory                |
| Host/Group vars   | Organized variable files            |
| Role vars         | Inside roles                        |
| Facts             | System-generated variables          |
| Registered vars   | Output of tasks                     |
| set_fact          | Runtime variables                   |
| Extra vars        | CLI input (highest priority)        |
| Env vars          | From environment                    |
| Prompt vars       | User input at runtime               |

---

## Real-World Example  

“In our projects, we used group_vars for environment-specific configs, role defaults for base values, and extra-vars in CI/CD pipelines to override values during deployment.”

---

## Key Takeaways  

- Variables come from multiple sources  
- Each has different scope and priority  
- Extra-vars override everything  

---

## Interview-Ready Summary  

“Ansible supports multiple types of variables such as playbook vars, inventory vars, role vars, facts, registered vars, and extra-vars. These variables differ in scope and precedence, allowing flexible and dynamic configuration management.”

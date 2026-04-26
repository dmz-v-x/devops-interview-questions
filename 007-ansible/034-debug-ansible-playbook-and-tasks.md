### Question  
How do you debug an Ansible playbook and tasks? (Verbose mode)

---

### Short Explanation of the Question  

This question checks your ability to troubleshoot Ansible executions using built-in debugging techniques like verbose mode, logging, and debug modules.

---

### Answer  

You can debug Ansible playbooks using verbose mode (`-v`, `-vv`, `-vvv`, `-vvvv`), which increases the level of detail in the output. Additionally, you can use the debug module, check logs, and isolate failing tasks to identify issues effectively.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### 1. Use Verbose Mode (Primary Method)

Ansible provides multiple verbosity levels:

```bash
ansible-playbook playbook.yml -v
ansible-playbook playbook.yml -vv
ansible-playbook playbook.yml -vvv
ansible-playbook playbook.yml -vvvv
```

---

### Verbosity Levels  

- `-v` → Basic task execution details  
- `-vv` → More detailed output  
- `-vvv` → Shows task-level debugging  
- `-vvvv` → Full debug (SSH, WinRM, connection details)  

---

### 2. Use debug Module  

Print variables and values:

```yaml
- name: Debug variable
  debug:
    var: my_variable
```

---

#### Print Custom Message  

```yaml
- debug:
    msg: "Value is {{ my_variable }}"
```

---

### 3. Check Failed Task Output  

- Look at:
  - Error message  
  - Return code  
  - Module output  

---

### 4. Use --step Mode  

Run tasks step-by-step:

```bash
ansible-playbook playbook.yml --step
```

---

### 5. Use --start-at-task  

Start execution from a specific task:

```bash
ansible-playbook playbook.yml --start-at-task="Install nginx"
```

---

### 6. Check Syntax Before Running  

```bash
ansible-playbook playbook.yml --syntax-check
```

---

### 7. Dry Run (Check Mode)  

```bash
ansible-playbook playbook.yml --check
```

---

### 8. Logging  

Enable logging in ansible.cfg:

```ini
log_path=/var/log/ansible.log
```

---

### Real-World Example  

“When debugging a failed deployment, I used `-vvv` to get detailed output and identify a variable mismatch. I added debug tasks to print variable values and used `--start-at-task` to rerun only the failing section, which helped quickly isolate and fix the issue.”

---

### Key Takeaways  

- Verbose mode is the primary debugging tool  
- Use debug module to inspect variables  
- Use step and start-at-task for controlled execution  
- Always check syntax and use dry-run  

---

### Interview-Ready Summary  

“To debug Ansible playbooks, I primarily use verbose mode with flags like `-vvv` or `-vvvv` to get detailed execution logs. I also use the debug module to print variable values, and options like `--step` or `--start-at-task` to isolate issues. This helps quickly identify and fix problems in playbooks.”

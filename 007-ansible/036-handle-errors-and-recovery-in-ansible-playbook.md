### Question  
How do you handle error handling and recovery in Ansible playbooks? (ignore_errors, failed_when, and block statements)

---

### Short Explanation of the Question  

This question evaluates how you control failures in Ansible, customize error conditions, and implement recovery mechanisms to make playbooks more resilient.

---

### Answer  

In Ansible, error handling is managed using features like `ignore_errors`, `failed_when`, and `block/rescue/always`. These allow you to control task failures, define custom failure conditions, and implement recovery logic when something goes wrong.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### 1. ignore_errors  

- Allows playbook to continue even if a task fails  

---

#### Example  

```yaml
- name: Try installing a package
  apt:
    name: nginx
    state: present
  ignore_errors: yes
```

---

### When to Use  

- Non-critical tasks  
- Optional steps  

---

### Limitation  

- Error is ignored completely (not ideal for controlled recovery)  

---

### 2. failed_when  

- Define custom failure conditions  
- Override default success/failure logic  

---

#### Example  

```yaml
- name: Check application response
  command: curl -s http://localhost
  register: result
  failed_when: result.rc != 0 or "error" in result.stdout
```

---

### Use Cases  

- Fail based on:
  - Output content  
  - Exit codes  
  - Custom logic  

---

### 3. block / rescue / always (Best Practice)  

Used for structured error handling.

---

#### Example  

```yaml
- name: Error handling with block
  block:
    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started

  rescue:
    - name: Handle failure
      debug:
        msg: "Installation failed, taking corrective action"

  always:
    - name: Always run this
      debug:
        msg: "Cleanup or logging"
```

---

### How It Works  

1. block → main tasks  
2. If failure occurs → rescue runs  
3. always → runs regardless of success/failure  

---

### 4. Additional Useful Techniques  

---

#### Register + Conditional Handling  

```yaml
- name: Run command
  command: some_command
  register: result
  ignore_errors: yes

- name: Handle failure
  debug:
    msg: "Command failed"
  when: result.rc != 0
```

---

### Real-World Example  

“In one deployment, a package installation occasionally failed due to network issues. We used a block with rescue to retry the installation and log the failure. This ensured the playbook didn’t completely stop and could recover automatically.”

---

### Key Takeaways  

- `ignore_errors` → skip failure (use cautiously)  
- `failed_when` → customize failure conditions  
- `block/rescue/always` → structured error handling and recovery  

---

### Interview-Ready Summary  

“I handle errors in Ansible using ignore_errors for non-critical tasks, failed_when to define custom failure conditions, and block-rescue-always for structured error handling and recovery. In practice, I prefer block-rescue because it allows controlled recovery instead of silently ignoring failures.”

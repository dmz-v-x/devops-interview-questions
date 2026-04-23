### Question
How can you continue Ansible Playbook execution even if some tasks fail?

### Answer

By default, Ansible stops execution when a task fails. However, there are multiple ways to **continue execution even after failures**, depending on how much control and flexibility you need.

---

### 1. Using `ignore_errors`

#### Purpose
Allows the playbook to continue even if a specific task fails.

#### Example

```
- name: Install optional package
  yum:
    name: somepackage
    state: present
  ignore_errors: yes

- name: Start web service
  service:
    name: httpd
    state: started
```

#### Key Points

- If the package installation fails, the next task still runs  
- Simple and quick solution  
- No custom error handling  

#### When to Use

- Optional tasks  
- Non-critical steps  

---

### 2. Using `block`, `rescue`, and `always`

#### Purpose
Provides structured error handling with control over what happens on failure.

#### Example

```
- block:
    - name: Install primary package
      yum:
        name: mypackage
        state: present

    - name: Configure package
      template:
        src: config.j2
        dest: /etc/mypackage.conf

  rescue:
    - name: Log failure
      debug:
        msg: "Primary package installation failed, continuing playbook."

  always:
    - name: Start service
      service:
        name: mypackage
        state: started
```

#### Key Points

- `block` → main tasks  
- `rescue` → runs only if a task in block fails  
- `always` → runs regardless of success or failure  

#### When to Use

- Critical workflows  
- When fallback or recovery logic is needed  
- When you want controlled error handling  

---

### 3. Using `failed_when`

#### Purpose
Overrides Ansible’s default failure conditions.

#### Example

```
- name: Run command that may fail
  command: /usr/bin/might_fail
  failed_when: false
```

#### Key Points

- Prevents task from being marked as failed  
- Useful when non-zero exit codes are acceptable  
- Can be combined with `register` for custom checks  

---

### 4. Quick Comparison

| Method | Use Case | Notes |
|---|---|---|
| `ignore_errors: yes` | Simple, non-critical tasks | Continues execution, no handling |
| `block/rescue/always` | Controlled error handling | Best for complex or critical flows |
| `failed_when` | Custom failure logic | Flexible, condition-based control |

---

### Final Summary

- Use **`ignore_errors`** for simple, non-critical failures  
- Use **`block/rescue/always`** for structured error handling and recovery  
- Use **`failed_when`** when you want to redefine what counts as a failure  

These approaches allow you to build resilient and fault-tolerant Ansible playbooks.

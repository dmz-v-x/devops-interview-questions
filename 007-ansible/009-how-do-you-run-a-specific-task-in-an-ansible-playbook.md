### Question  
How do you run a specific task in an Ansible playbook?

---

### Answer

There are multiple ways to run a specific task in an Ansible playbook depending on your use case.

---

### 1. Using Tags (Most Common and Recommended)

#### What are Tags?
Tags allow you to label tasks and selectively execute them.

#### Example Playbook

```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present
  tags: install

- name: Start Nginx
  service:
    name: nginx
    state: started
  tags: start
```

#### Run Only a Specific Task

```bash
ansible-playbook site.yml --tags install
```

#### Skip a Specific Task

```bash
ansible-playbook site.yml --skip-tags start
```

#### Key Points

- Most widely used method  
- Clean and reusable  
- Useful for large playbooks  

---

### 2. Using --start-at-task

#### Purpose
Start execution from a specific task name.

#### Example

```bash
ansible-playbook site.yml --start-at-task="Start Nginx"
```

#### Key Points

- Requires exact task name  
- Useful for debugging or resuming execution  
- Executes all tasks from that point onward  

---

### 3. Using --step Mode

#### Purpose
Execute playbook interactively, step by step.

#### Example

```bash
ansible-playbook site.yml --step
```

#### How It Works

- Prompts before each task  
- You can choose:
  - yes → run task  
  - no → skip task  

#### Key Points

- Useful for learning and debugging  
- Not commonly used in automation pipelines  

---

### Quick Comparison

| Method            | Use Case                         | Notes                          |
|------------------|----------------------------------|--------------------------------|
| Tags             | Run specific tasks               | Most common and recommended    |
| --start-at-task  | Resume from a task               | Needs exact task name          |
| --step           | Debug interactively              | Manual confirmation required   |

---

### Interview-Ready Summary

“In Ansible, the most common way to run a specific task is by using tags. For example, I can assign `tags: install` to a task and run:

```bash
ansible-playbook site.yml --tags install
```

Alternatively, I can use `--start-at-task` to begin execution from a specific task, or `--step` to run tasks interactively one by one.”

### Question  
Does Ansible support parallel execution of tasks?

---

### Short Explanation of the Question  

This question checks whether you understand how Ansible executes tasks across multiple hosts and how parallelism is controlled.

---

### Answer  

Yes, Ansible supports parallel execution across multiple hosts. By default, it runs tasks in parallel on multiple hosts using a configurable number of forks, while tasks within a single host are executed sequentially.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### How Ansible Executes Tasks  

- Across hosts → Parallel  
- Within a host → Sequential  

Example:

If you have 10 servers:

- Ansible can run the same task on multiple servers simultaneously  
- But on each server, tasks run one after another  

---

### 1. Forks (Parallelism Control)

- Forks define how many hosts Ansible can handle in parallel  

Default:

```bash
forks = 5
```

---

#### Increase Forks  

```bash
ansible-playbook playbook.yml -f 10
```

---

### 2. Strategy (Execution Behavior)

---

#### Linear (Default)

- Runs task-by-task across all hosts  
- Example:
  - Task 1 → all hosts  
  - Task 2 → all hosts  

---

#### Free Strategy

- Hosts run tasks independently (no waiting)

```yaml
- hosts: all
  strategy: free
```

---

### 3. Async Execution (Background Tasks)

Run long tasks asynchronously:

```yaml
- name: Run long task
  command: sleep 60
  async: 120
  poll: 0
```

- async → max runtime  
- poll: 0 → fire-and-forget  

---

### 4. Serial Execution (Controlled Rolling Updates)

Limit parallel execution:

```yaml
- hosts: web
  serial: 2
```

- Runs on 2 hosts at a time  

---

### Real-World Example  

“In one deployment, we had 50 servers. We increased forks to speed up execution and used serial for rolling updates to avoid downtime. For long-running tasks like backups, we used async to prevent blocking the playbook.”

---

### Key Takeaways  

- Parallel across hosts  
- Sequential within a host  
- Controlled using:
  - forks  
  - strategy  
  - async  
  - serial  

---

### Interview-Ready Summary  

“Yes, Ansible supports parallel execution across hosts using forks. By default, it runs tasks in parallel on multiple machines while executing tasks sequentially on each host. We can control this behavior using forks, strategies like free, async tasks, or serial execution for rolling updates.”

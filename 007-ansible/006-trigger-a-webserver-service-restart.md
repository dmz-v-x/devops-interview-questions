### Question
How do you trigger a webserver service restart in Ansible only when there is a configuration change, and skip it otherwise?

### Answer

In Ansible, this is achieved using **handlers**. Handlers are special tasks that run **only when notified by other tasks**, and only if those tasks report a change.

---

### 1. Define a Handler

#### Purpose
Create a restart task that runs only when explicitly triggered.

#### Location
Typically defined in:

```
roles/<role_name>/handlers/main.yml
```

#### Example

```
---
- name: restart webserver
  service:
    name: httpd
    state: restarted
```

#### Key Points

- This does not run automatically  
- It runs only when notified  
- Ensures controlled execution  

---

### 2. Notify the Handler from Tasks

#### Purpose
Trigger the handler only when a task changes something on the system.

#### Example

```
- name: Deploy Apache configuration
  template:
    src: httpd.conf.j2
    dest: /etc/httpd/conf/httpd.conf
  notify: restart webserver

- name: Deploy custom index.html
  template:
    src: index.html.j2
    dest: /var/www/html/index.html
  notify: restart webserver
```

#### How It Works

- If the file content changes → task status = **changed**  
- If no change → task status = **ok**  

#### Result

- Changed → handler is triggered  
- No change → handler is skipped  

---

### 3. Playbook Example Using Role

```
- hosts: webservers
  become: yes
  roles:
    - apache
```

#### Structure Inside Role

- `tasks/main.yml` → deploys configuration and files  
- `handlers/main.yml` → contains restart logic  

---

### 4. Execution Flow (Very Important)

1. Task runs (e.g., template deployment)  
2. Ansible checks if the system state changed  
3. If changed → handler is notified  
4. Handler runs at the **end of the playbook**  
5. If no changes → handler does not run  

---

### 5. Advantages

- Avoids unnecessary service restarts  
- Improves performance and efficiency  
- Maintains idempotency (no repeated actions if nothing changed)  
- Ensures services restart only when required  

---

### Final Summary

In Ansible, you use **handlers with notify** to restart services only when configuration changes occur. If no changes are detected, the handler is skipped automatically, making automation efficient and reliable.

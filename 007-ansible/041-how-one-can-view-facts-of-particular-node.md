### Question  
How can you view facts of a particular node in Ansible?

---

### Short Explanation of the Question  

This question tests your understanding of how to retrieve system information (facts) from a specific managed host.

---

### Answer  

You can view facts of a particular node using the **setup module** in Ansible. This module gathers and displays all system information (facts) about the target host.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

## Method 1: Using Ad-hoc Command (Most Common)  

```bash
ansible <host> -m setup
```

---

### Example  

```bash
ansible web1 -m setup
```

---

### What It Does  

- Connects to the host  
- Runs the setup module  
- Returns all facts in JSON format  

---

## Filter Specific Facts  

```bash
ansible web1 -m setup -a "filter=ansible_os_family"
```

---

### Example Output  

```json
"ansible_os_family": "Debian"
```

---

## Method 2: Using Playbook  

```yaml
- hosts: web1
  tasks:
    - name: Print all facts
      debug:
        var: ansible_facts
```

---

## Method 3: Debug Specific Fact  

```yaml
- hosts: web1
  tasks:
    - name: Show IP address
      debug:
        msg: "{{ ansible_default_ipv4.address }}"
```

---

## Notes  

- Facts are gathered automatically when:
  
```yaml
gather_facts: yes
```

- If disabled:
  
```yaml
gather_facts: no
```

→ setup module must be run manually  

---

## Real-World Example  

“When troubleshooting environment-specific issues, I used the setup module to check OS type, network details, and memory configuration of a particular node before applying playbooks.”

---

## Key Takeaways  

- Use setup module to fetch facts  
- Can filter specific facts  
- Useful for debugging and validation  

---

## Interview-Ready Summary  

“To view facts of a particular node, I use the setup module with an ad-hoc command like ansible <host> -m setup. It returns detailed system information, and I can filter specific facts if needed for debugging or validation.”

### Question  
Can you place Ansible variable sources in the order of precedence?

---

### Short Explanation of the Question  

This question tests your understanding of how Ansible resolves conflicts when the same variable is defined in multiple places.

---

### Answer  

Yes, Ansible follows a defined order of precedence where variables defined later (or at higher priority levels) override earlier ones. Below is the order from lowest to highest precedence.

---

### Detailed Explanation of the Answer for Readers’ Understanding  

---

### Variable Precedence (Low → High)

1. Role defaults (`roles/.../defaults/main.yml`)  
2. Inventory variables (group_vars, host_vars)  
3. Playbook variables (`vars:` in play)  
4. Task variables (`vars:` in task)  
5. Block variables  
6. Role variables (`roles/.../vars/main.yml`)  
7. Include/import variables  
8. Set facts (`set_fact`)  
9. Extra variables (`-e` or `--extra-vars`)  

---

### Important Notes  

- Extra vars (`-e`) have the **highest precedence**  
- Role defaults have the **lowest precedence**  
- Variables closer to execution (task level) override broader scope variables  

---

### Example  

```yaml
# inventory
app_port=8080

# playbook
vars:
  app_port: 9090

# CLI
ansible-playbook play.yml -e "app_port=7070"
```

---

### Result  

- Final value used → **7070** (because extra-vars override everything)

---

### Real-World Tip  

- Use:
  - defaults → for configurable values  
  - vars → for fixed/internal values  
  - extra-vars → for overrides in CI/CD  

---

### Key Takeaways  

- Precedence determines which value wins  
- Higher level overrides lower level  
- Extra vars always win  

---

### Interview-Ready Summary  

“Yes, Ansible has a defined variable precedence. It starts with role defaults at the lowest level and goes up through inventory, playbook, and task variables, with extra-vars having the highest precedence. This ensures predictable behavior when the same variable is defined in multiple places.”

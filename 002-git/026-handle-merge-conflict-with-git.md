### Question  
How do you handle merge conflicts in Git?

---

### Answer  

---

### 1. High-Level Approach

When I encounter a merge conflict:

- I **identify the conflicting files**  
- Understand both sides of the changes  
- Manually resolve conflicts  
- Stage and complete the merge/rebase  

---

### 2. Why Merge Conflicts Happen

- Same lines modified in multiple branches  
- One branch deletes a file, another modifies it  
- Rebase overlaps with existing changes  

---

### 3. Step-by-Step Resolution

---

### Step 1: Identify Conflicts

During merge or rebase, Git shows:

```bash
Auto-merging app.py
CONFLICT (content): Merge conflict in app.py
```

---

### Step 2: Open and Resolve

Conflicted file looks like:

```text
<<<<<<< HEAD
print("Hello from main")
=======
print("Hello from feature-branch")
>>>>>>> feature-branch
```

---

#### What I do:

- Analyze both changes  
- Decide correct final logic  
- Remove conflict markers  
- Keep clean code  

---

### Step 3: Use Tools (Optional)

- CLI:
```bash
git diff
```

- GUI tools:
  - VS Code  
  - GitKraken  

---

### Step 4: Mark as Resolved

```bash
git add app.py
```

---

### Step 5: Complete Process

---

#### If using merge:

```bash
git commit
```

---

#### If using rebase:

```bash
git rebase --continue
```

---

### 4. Best Practices

- Pull latest changes before starting work  
- Use small, focused commits  
- Avoid long-lived branches  
- Communicate with team for overlapping work  

---

### 5. Key Takeaways

- Conflicts are normal in collaboration  
- Always understand changes before resolving  
- Use tools for clarity  
- Keep final code clean and correct  

---

### 6. Interview-Ready Summary

“When I encounter a merge conflict, I first identify the affected files, review both sets of changes, and manually resolve the conflict by choosing the correct logic. I then stage the resolved files and complete the merge or rebase. I also use tools like git diff or IDEs for better visibility and follow best practices to minimize conflicts.”

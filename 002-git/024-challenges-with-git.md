### Question  
Explain three challenges you faced while using Git in your work experience.

---

### Answer  

---

### 1. Merge Conflicts During Pulls

---

#### Problem:

- I frequently used:

```bash
git pull
```

- Without checking incoming changes  
- This often caused **merge conflicts**, especially in fast-moving branches  

---

#### Solution:

- Switched to:

```bash
git fetch
git merge
```

or

```bash
git rebase
```

---

#### Benefit:

- Better visibility of incoming changes  
- More control over conflict resolution  

---

### 2. Messy Commit History

---

#### Problem:

- Used `git merge` frequently in long-lived feature branches  
- Result:
  - Multiple unnecessary merge commits  
  - Hard-to-read commit history  

---

#### Solution:

- Started using:

```bash
git rebase
```

(before pushing changes)

---

#### Benefit:

- Clean, linear commit history  
- Easier code review and debugging  

---

### 3. Confusion Between Fork and Clone (Open Source)

---

#### Problem:

- Initially used:

```bash
git clone
```

- Could not push changes to original repository  

---

#### Solution:

- Learned to use **fork workflow**:

1. Fork repository on GitHub  
2. Clone forked repo  
3. Push changes to fork  
4. Create Pull Request  

---

#### Benefit:

- Proper open-source contribution workflow  
- Ability to submit changes safely  

---

### 4. Pre-Commit Hooks (Additional Challenge)

---

#### Problem:

- Code inconsistencies:
  - Formatting issues  
  - Missed lint checks  

---

#### Solution:

- Implemented **pre-commit hooks**  

---

#### Benefit:

- Automatic checks before commits  
- Improved code quality  
- Reduced CI failures  

---

### 5. Key Takeaways

- Use `git fetch` instead of blind `git pull`  
- Prefer `git rebase` for clean history  
- Understand fork vs clone in open source  
- Use pre-commit hooks for consistency  

---

### 6. Interview-Ready Summary

“I faced challenges like merge conflicts due to direct git pull usage, messy commit history from frequent merges, and confusion between fork and clone while contributing to open source. I resolved these by using git fetch and rebase for better control, adopting a clean commit strategy, and following the proper fork-based workflow. I also implemented pre-commit hooks to maintain code quality.”

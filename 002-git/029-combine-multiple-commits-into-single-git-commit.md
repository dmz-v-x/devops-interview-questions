### Question  
How do you combine multiple commits into a single commit in Git?

---

### Answer  

I use **interactive rebase** to squash multiple commits into a single, clean commit before pushing or creating a PR.

---

### 1. Why Squash Commits?

- Keeps Git history clean  
- Groups related changes into one logical commit  
- Makes code review and debugging easier  

---

### 2. Example Scenario

Suppose I have 4 commits:

```bash
git log --oneline
abc123 Fix typo  
def456 Add input validation  
ghi789 Update error message  
jkl012 Initial work on login form  
```

---

### 3. Start Interactive Rebase

```bash
git rebase -i HEAD~4
```

---

### 4. Editor Opens

```text
pick jkl012 Initial work on login form
pick ghi789 Update error message
pick def456 Add input validation
pick abc123 Fix typo
```

---

### 5. Change to Squash

```text
pick jkl012 Initial work on login form
squash ghi789 Update error message
squash def456 Add input validation
squash abc123 Fix typo
```

---

### 6. Final Step

- Write a new commit message:

```
Add login form with validation and error handling
```

- Save and exit  

---

### 7. Push Changes

---

#### If NOT pushed before:

```bash
git push origin branch-name
```

---

#### If already pushed:

```bash
git push origin branch-name --force
```

---

### 8. Important Note

- Use `--force` carefully  
- Avoid force push on shared branches  

---

### 9. Key Takeaways

- Use `git rebase -i` to squash commits  
- Keep history clean and meaningful  
- Best practice before merging PRs  

---

### 10. Interview-Ready Summary

“To combine multiple commits into one, I use interactive rebase with git rebase -i, then squash the commits into a single meaningful commit. This helps maintain a clean and readable Git history, especially before raising a pull request or merging into the main branch.”

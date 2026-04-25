### Question  
Explain 10 Git commands that you use on a day-to-day basis. What are they used for?

---

### Answer  

---

### 1. `git clone`

```bash
git clone https://github.com/org/repo.git
```

- Creates a **local copy** of a remote repository  
- Used when:
  - Starting a new project  
  - Joining an existing codebase  

---

### 2. `git status`

```bash
git status
```

- Shows:
  - Staged changes  
  - Unstaged changes  
  - Untracked files  

- Helps understand current working state  

---

### 3. `git add`

```bash
git add file.py
git add .
```

- Stages changes before commit  
- Selects what should go into the next commit  

---

### 4. `git commit`

```bash
git commit -m "Fix login bug"
```

- Saves a snapshot of staged changes  
- Adds a meaningful message for tracking  

---

### 5. `git push`

```bash
git push origin feature-branch
```

- Uploads local commits to remote repository  
- Used after:
  - Commit  
  - Merge  

---

### 6. `git pull`

```bash
git pull origin main
```

- Fetches + merges changes from remote  
- Keeps local branch updated  

---

### 7. `git fetch`

```bash
git fetch origin
```

- Downloads changes from remote  
- Does NOT merge automatically  
- Useful for:
  - Reviewing changes before integrating  

---

### 8. `git branch`

```bash
git branch
git branch feature/login
```

- Lists branches  
- Creates new branches  
- Helps in feature-based development  

---

### 9. `git checkout`

```bash
git checkout main
git checkout -b hotfix/typo
```

- Switches between branches  
- Can create + switch in one command  

---

### 10. `git rebase`

```bash
git rebase main
```

- Re-applies commits on top of another branch  
- Used to:
  - Keep history clean  
  - Avoid unnecessary merge commits  

---

### 11. Key Takeaways

- These commands cover:
  - Cloning  
  - Tracking changes  
  - Committing  
  - Syncing  
  - Branching  
  - History management  

---

### 12. Interview-Ready Summary

“I regularly use commands like git clone to get repositories, git status to check changes, git add and commit to save work, and git push/pull to sync with remote. I also use git fetch for safe updates, git branch and checkout for managing branches, and git rebase to maintain a clean commit history.”

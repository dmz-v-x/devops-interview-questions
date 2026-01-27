### Q: What is the difference between `git fetch` and `git pull`, and when would you use each?

**Answer:**

`git fetch` and `git pull` are both used to retrieve updates from a remote repository, but they differ in how those updates are applied to your local code.

---

### Git Fetch  
`git fetch` downloads the latest changes from the remote repository **without modifying your current branch or working directory**.

Example:
    
    git fetch origin

What it does:
- Retrieves new commits, branches, and tags from the remote  
- Updates remote-tracking branches (like `origin/main`)  
- Does **not** merge changes into your local branch  

When to use `git fetch`:
- When you want to review incoming changes before applying them  
- When preparing for a manual merge or rebase  
- When you want to avoid unexpected changes in your working branch  

> **Depth addition:** Fetch is a safe operation—it never alters your local code, making it ideal in collaborative or critical workflows.

---

### Git Pull  
`git pull` fetches changes from the remote repository **and immediately merges them** into your current branch.

Example:
    
    git pull origin main

Internally, this is equivalent to:
    
    git fetch origin  
    git merge origin/main

What it does:
- Downloads the latest changes  
- Automatically merges them into the current branch  

When to use `git pull`:
- When you are sure your branch is ready to receive changes  
- When you want a quick sync with the remote branch  
- In simple workflows with minimal merge conflict risk  

> **Clarification:** `git pull` can also be configured to rebase instead of merge (`git pull --rebase`), which some teams prefer.

---

### Key Difference (Interview Focus)

- **git fetch** → Downloads changes only, gives you control  
- **git pull** → Downloads and merges changes immediately  

---

### Summary (Interview-Friendly Line)

Use `git fetch` when you want to review and control incoming changes before merging, and use `git pull` when you’re ready to immediately sync and merge remote changes into your local branch.

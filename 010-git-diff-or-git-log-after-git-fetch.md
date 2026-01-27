### Q: How do you use `git diff` or `git log` after running `git fetch`?

**Answer:**

After running `git fetch`, Git downloads the latest changes from the remote repository but does **not** merge them into your current branch. This allows you to safely inspect what has changed before deciding to merge or rebase.

---

### Step 1: Fetch the latest changes

    git fetch origin

This updates remote-tracking branches such as `origin/main` without modifying your local branch.

---

### Using `git log` after `git fetch`

You can use `git log` to see **what commits exist on the remote branch but not on your local branch**.

Example:

    git log HEAD..origin/main

What this shows:
- Commits that are present on `origin/main`
- Commits that are **not yet in your local branch**

This helps you:
- Review commit messages  
- Understand the scope of incoming changes  
- Decide whether you want to merge or rebase  

> **Interview insight:** This is commonly used before pulling changes in critical branches.

---

### Using `git diff` after `git fetch`

You can use `git diff` to see **exact code-level differences** between your local branch and the remote branch.

Example:

    git diff HEAD..origin/main

What this shows:
- Line-by-line code changes  
- Files that were modified, added, or removed  

This is useful when:
- You want to inspect changes carefully  
- You want to anticipate merge conflicts  
- You want to review changes before pulling them  

---

### Typical Safe Workflow (Interview-Approved)

1. Fetch remote changes:

       git fetch origin

2. Review commit history:

       git log HEAD..origin/main

3. Review code differences:

       git diff HEAD..origin/main

4. Merge or rebase when ready:

       git merge origin/main  
       (or)  
       git rebase origin/main  

---

### Why this approach matters

Using `git fetch` with `git log` and `git diff`:
- Prevents surprise merges  
- Gives full visibility into incoming changes  
- Is considered a best practice in professional teams  

---

### Summary (Interview-Friendly Line)

After `git fetch`, I use `git log` to review incoming commits and `git diff` to inspect code changes before merging, which gives me full control and avoids unexpected issues.

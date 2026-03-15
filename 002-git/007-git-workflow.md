### Q: Explain a common Git workflow used in teams.

**Answer:**

A common Git workflow defines how developers collaborate, manage code changes, and safely deliver features using branches, pull requests, and reviews. Below is a typical **feature-branch-based Git workflow**, explained step by step as expected in interviews.

---

### 1. Clone the Repository  
The first step is to get a local copy of the remote repository.

    git clone <repo-url>

This creates:
- A local working copy of the code
- A connection to the remote repository (`origin`)

---

### 2. Create a Feature Branch  
Developers never work directly on `main` (or `develop`). Instead, they create a separate feature branch.

    git checkout -b feature/my-feature

This:
- Isolates work for a specific feature or bugfix  
- Keeps the main branch stable  
- Enables parallel development  

> **Interview note:** Feature branches are short-lived and focused on one task.

---

### 3. Make Changes and Commit  
Code changes are made incrementally and committed with meaningful messages.

    git add .
    git commit -m "Add login form validation"

Best practices:
- Small, logical commits  
- Clear commit messages  
- One concern per commit  

---

### 4. Pull Latest Changes (Rebase Preferred)  
Before pushing, the branch is updated with the latest changes from the main branch.

    git pull origin main --rebase

Take the latest main branch from origin and replay my current branch’s commits on top of it

This:
- Brings your branch up to date  
- Avoids unnecessary merge commits  
- Keeps history clean and linear  

> **Depth addition:** Rebasing is commonly used on local feature branches before opening a PR.

---

### 5. Push Your Feature Branch  
Once the branch is up to date, it is pushed to the remote repository.

    git push origin feature/my-feature

This makes your branch available to:
- Other team members  
- CI pipelines  
- Pull Request creation  

---

### 6. Open a Pull Request (PR) / Merge Request (MR)  
A Pull Request is created to merge the feature branch into `main` or `develop`.

Purpose:
- Code review  
- Automated testing  
- Discussion and feedback  

> **Interview insight:** PRs enforce quality, collaboration, and accountability.

---

### 7. Code Review and Testing  
Team members:
- Review code for quality and standards  
- Suggest improvements  
- Ensure CI tests pass  

Changes may be requested and updated commits pushed to the same branch.

---

### 8. Merge the Branch  
After approval and successful tests, the feature branch is merged into the target branch.

Common merge strategies:
- Merge commit  
- Squash merge  
- Rebase & merge  

---

### 9. Delete the Feature Branch  
Once merged, the feature branch is deleted to keep the repository clean.

    git branch -d feature/my-feature
    git push origin --delete feature/my-feature

This:
- Reduces clutter  
- Prevents confusion  
- Encourages short-lived branches  

---

### Summary (Interview-Friendly Line)

A common Git workflow involves creating a feature branch, making and committing changes, rebasing with the latest main branch, pushing the branch, opening a pull request for review, merging after approval, and finally cleaning up the branch.

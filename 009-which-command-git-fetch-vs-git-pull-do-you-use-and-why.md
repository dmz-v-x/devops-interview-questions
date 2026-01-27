### Q: Which command do you use more often — `git fetch` or `git pull`, and why?

**Answer:**

I mostly use **`git pull`** because it streamlines my workflow by fetching and merging remote changes in a single step. It helps me stay up to date quickly, especially when working on fast-moving branches.

`git pull` is essentially a shortcut that performs both:
- `git fetch`
- `git merge`

For example:

    git pull origin main

This keeps my local branch synchronized with the remote without requiring extra commands.

I typically prefer `git pull` when:
- I’m working alone or in a small team where merge conflicts are rare  
- I’m contributing to a feature branch that others are not actively modifying  
- I want to frequently sync the latest changes for testing or deployment  

To avoid issues, I make sure to commit or stash local changes before pulling. If I expect significant upstream changes or want to review commits before merging, I switch to using `git fetch` temporarily.

> **Depth addition:** While `git pull` is convenient, understanding what it does internally is important to avoid unintended merges.

---

### Summary (Interview-Friendly Line)

I usually use `git pull` for day-to-day work because it quickly keeps my branch in sync, but I switch to `git fetch` when I need more control or want to review changes before merging.

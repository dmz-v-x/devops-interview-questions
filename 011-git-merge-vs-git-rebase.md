### Q: What is the difference between `git merge` and `git rebase`? When would you use each?

**Answer:**

`git merge` and `git rebase` are both used to integrate changes from one branch into another, but they do so in very different ways and result in different commit histories.

Understanding this difference is important for maintaining clean history and avoiding collaboration issues.

---

## 1. What is `git merge`?

`git merge` integrates changes from one branch into another by creating a **new merge commit**. It preserves the complete history of both branches exactly as they happened.

### Example scenario
You have two branches:
- `main`
- `feature` (branched earlier from `main`)

Command:

    git checkout feature
    git merge main

Here we're updating feature with the latest changes from main. Often done to keep a feature branch up to date.

### Resulting history:

    A---B---C (main)
         \
          D---E---F (feature)
                 \
                  G (merge commit)

### Key characteristics of `git merge`:
- Creates a **merge commit**
- Preserves full branch history
- Does **not rewrite commits**

### Pros:
- Preserves full context and timeline
- Safe for team collaboration
- Ideal for long-lived or shared branches

### Cons:
- History can become cluttered
- Many merge commits can make `git log` harder to read

---

## 2. What is `git rebase`?

`git rebase` moves your branch on top of another branch by **replaying your commits** one by one. This rewrites commit history to create a clean, linear sequence.

### Example:

    git checkout feature
    git rebase main

### Resulting history:

    A---B---C (main)
                 \
                  D'---E'---F' (rebased feature)

> The commits appear as if the feature branch was created from the latest `main`.

### Key characteristics of `git rebase`:
- Rewrites commit history
- No merge commit is created
- Produces a linear history

### Pros:
- Clean and easy-to-read history
- Easier debugging with `git log` and `git bisect`
- Ideal before merging feature branches

### Cons:
- Rewrites history (commit hashes change)
- Dangerous if used on shared/public branches
- Can cause problems for teammates if misused

---

## 3. Conflict Handling Difference

- **Merge:** Conflicts are resolved once during the merge.
- **Rebase:** Conflicts may occur **for each commit** being replayed.

---

## 4. When to Use `git merge` vs `git rebase`

| Scenario | Recommended Command |
|--------|---------------------|
| Shared or public branches | `git merge` |
| Working alone on a feature | `git rebase` |
| Want full historical context | `git merge` |
| Want a clean, linear history | `git rebase` |
| Safety is more important than cleanliness | `git merge` |
| Cleaning commits before a PR | `git rebase` |

---

## 5. Quick Comparison Table

| Feature | `git merge` | `git rebase` |
|------|------------|--------------|
| Purpose | Combines branches | Rewrites history |
| Commit history | Preserves full history | Linear, rewritten |
| Merge commit | Yes | No |
| Safe for public branches | ✅ Yes | ❌ No |
| Conflict resolution | Once | Per commit |
| Best use case | Team collaboration | Local feature cleanup |

---

## ⚠️ Important Interview Note

**Never rebase a shared or public branch** that others are working on. Rebasing rewrites history and can break teammates’ work.

---

## Summary (Interview-Friendly Line)

Use `git merge` when you want to safely combine branches and preserve full history, especially in shared branches. Use `git rebase` when working on local or short-lived feature branches to create a clean, linear commit history before merging.

> Git merge combines two branches and creates a new merge commit, preserving the full history.

> Git rebase moves your branch commits on top of another branch, creating a cleaner, linear history.

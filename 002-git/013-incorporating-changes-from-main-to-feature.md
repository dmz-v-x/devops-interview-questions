### Question
You are working on a feature branch and need to incorporate the latest changes from the `main` branch into your feature branch. How would you do this?

### Answer

When working on a feature branch, it is important to regularly update it with the latest changes from the `main` branch. This ensures your code stays compatible with recent updates and reduces the risk of large merge conflicts later.

There are two common ways to incorporate changes from `main` into a feature branch:

- **Merge**
- **Rebase**

---

### Method 1: Merge `main` into the Feature Branch

This method merges the latest changes from the `main` branch into your feature branch while preserving the full commit history.

#### Step 1: Switch to your feature branch

    git checkout feature-xyz

---

#### Step 2: Fetch the latest changes from the remote repository

    git fetch origin

This updates your local references to the latest commits in the remote repository.

---

#### Step 3: Merge the latest `main` branch into your feature branch

    git merge origin/main

This merges the changes from `main` into your feature branch.

---

#### Pros of Using Merge

- Preserves the full history of both branches
- Safe to use on shared branches
- No rewriting of commit history

---

#### Cons of Using Merge

- Creates a **merge commit**
- Can clutter the commit history if used frequently

---

### Method 2: Rebase the Feature Branch onto `main`

Rebasing rewrites the feature branch history so that it appears as if the feature branch was created from the latest version of `main`.

#### Step 1: Switch to your feature branch

    git checkout feature-xyz

---

#### Step 2: Fetch the latest changes

    git fetch origin

---

#### Step 3: Rebase your branch onto the updated `main`

    git rebase origin/main

Git will reapply your feature branch commits on top of the latest `main` branch.

---

#### Pros of Using Rebase

- Creates a **clean, linear commit history**
- Easier to understand project history
- Avoids unnecessary merge commits

---

#### Cons of Using Rebase

- Rewrites commit history
- Can cause issues if the branch is already shared with other developers

---

### Handling Conflicts

If conflicts occur during merge or rebase, Git pauses the process so you can resolve them.

Resolve the conflicts in the affected files, then run:

For rebase:

    git add <resolved-file>
    git rebase --continue

For merge:

    git add <resolved-file>
    git commit

---

### Final Step: Push the Updated Feature Branch

After updating your branch, push it to the remote repository.

For merge workflow:

    git push origin feature-xyz

For rebase workflow (history rewritten):

    git push --force-with-lease origin feature-xyz

Using `--force-with-lease` is safer than `--force` because it ensures you do not overwrite someone else's work.

---

### Interview Summary

To incorporate changes from `main` into a feature branch, I can either merge or rebase. Merging preserves the full commit history and is safer for shared branches, while rebasing creates a cleaner linear history but rewrites commits and should be used carefully.

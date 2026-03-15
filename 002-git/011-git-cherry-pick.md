### Question
What is `git cherry-pick` and when would you use it?

### Answer

`git cherry-pick` is a Git command that allows you to **apply a specific commit from one branch onto another branch without merging the entire branch**.

This is useful when you only need **a particular change or fix**, rather than all the commits from the source branch.

In simple terms, cherry-pick lets you **copy one commit and apply it somewhere else**.

---

### Basic Syntax

    git cherry-pick <commit-hash>

The `<commit-hash>` represents the unique identifier of the commit you want to apply.

---

### Example Scenario

Suppose you have two branches:

- `main`
- `feature-branch`

A developer made a commit in `feature-branch` that fixes a bug, and the commit hash is:

    abc123

You want to apply this fix to the `main` branch **without merging the entire feature branch**.

#### Step 1: Switch to the target branch

    git checkout main

This is the branch where the commit will be applied.

---

#### Step 2: Cherry-pick the commit

    git cherry-pick abc123

Git will apply the changes introduced in commit `abc123` to the `main` branch as a new commit.

Now the bug fix exists in `main` without bringing all other commits from `feature-branch`.

---

### Handling Conflicts

Sometimes conflicts may occur during cherry-picking if the same files were modified in both branches.

In this case Git pauses the process so you can resolve the conflict manually.

After resolving conflicts:

    git add .

Then continue the cherry-pick process:

    git cherry-pick --continue

If necessary, the cherry-pick operation can also be aborted:

    git cherry-pick --abort

---

### Common Use Cases

`git cherry-pick` is typically used in situations such as:

- Applying a **hotfix from one branch to another**
- Bringing a **specific bug fix from `develop` into a `release` branch**
- Selecting only **specific commits instead of merging the full branch**
- Keeping release branches **clean and controlled**

---

### Best Practices

- Use cherry-pick when only a **small number of commits are required**
- Avoid excessive cherry-picking because it can create duplicated commits
- Ensure the selected commit is compatible with the target branch

---

### Interview Summary

`git cherry-pick` is used to apply a specific commit from one branch to another without merging the entire branch. It is commonly used for hotfixes or when only certain changes need to be applied.

Example:

    git checkout main
    git cherry-pick <commit-hash>

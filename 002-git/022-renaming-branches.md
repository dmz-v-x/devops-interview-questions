### Question
How do you rename a Git branch both locally and remotely?

### Answer

Renaming a Git branch involves updating the branch name in your **local repository** and then reflecting that change in the **remote repository**. This process ensures that the old branch name is removed and replaced with the new one.

The process typically includes four steps.

---

### Step 1: Rename the Branch Locally

If you are currently on the branch that you want to rename:

    git branch -m <new-branch-name>

Example:

    git branch -m feature-login

If you are on a different branch and want to rename another branch:

    git branch -m <old-branch-name> <new-branch-name>

Example:

    git branch -m feature-auth feature-login

Explanation:

- `-m` stands for **move**, which renames the branch.

---

### Step 2: Push the New Branch to the Remote Repository

After renaming the branch locally, push the new branch to the remote repository.

    git push origin <new-branch-name>

Example:

    git push origin feature-login

This creates the new branch on the remote repository.

---

### Step 3: Delete the Old Branch from the Remote

To avoid confusion and remove the old branch name from the remote repository, delete it.

    git push origin --delete <old-branch-name>

Example:

    git push origin --delete feature-auth

This removes the outdated branch reference from the remote repository.

---

### Step 4: Set Upstream Tracking (Optional but Recommended)

To ensure your local branch tracks the corresponding remote branch, set the upstream branch.

    git push --set-upstream origin <new-branch-name>

Example:

    git push --set-upstream origin feature-login

After this, future pushes can be done simply using:

    git push

---

### Final Workflow Example

    git branch -m feature-auth feature-login
    git push origin feature-login
    git push origin --delete feature-auth
    git push --set-upstream origin feature-login

---

### Interview Summary

To rename a Git branch locally and remotely, I first rename it locally using `git branch -m`, then push the new branch to the remote repository, delete the old remote branch, and optionally set the upstream tracking for the new branch.

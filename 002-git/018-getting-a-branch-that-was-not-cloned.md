### Question
If you cloned a repository without a specific branch and later need that branch, how would you fetch it?

### Answer

Sometimes a repository is cloned without all branches (for example when using `--single-branch`). If you later need another branch, you do **not need to re-clone the repository**. Instead, you can fetch the branch from the remote repository and create a local branch that tracks it.

---

### Step 1: Fetch Updates from the Remote Repository

First, fetch the latest information from the remote repository.

    git fetch origin

This command updates your local repository with information about branches available on the remote.

---

### Step 2: List Remote Branches

To see all branches available on the remote repository:

    git branch -r

This shows remote branches such as:

- origin/main
- origin/develop
- origin/feature/login-api

---

### Step 3: Fetch a Specific Branch

If you want to fetch a specific branch from the remote repository:

    git fetch origin <branch-name>

Example:

    git fetch origin feature/login-api

This downloads the branch data from the remote repository.

---

### Step 4: Create a Local Branch Tracking the Remote Branch

After fetching the branch, create a local branch that tracks the remote branch.

    git checkout -b <local-branch-name> origin/<branch-name>

Example:

    git checkout -b feature/login-api origin/feature/login-api

Explanation:

- `feature/login-api` becomes the local branch.
- It tracks the remote branch `origin/feature/login-api`.

You can now work on the branch locally.

---

### Best Practice

Fetching branches when needed avoids unnecessary downloads and keeps your local repository lightweight. This approach is especially useful when working with large repositories.

---

### Interview Summary

If I need a branch that wasn't cloned initially, I can fetch it using `git fetch origin <branch-name>` and then create a local tracking branch using `git checkout -b <local-branch-name> origin/<branch-name>`. This allows me to work on the branch without recloning the repository.

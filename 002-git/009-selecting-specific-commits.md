### Question
You have 50 commits in the `develop` branch, but only 5 specific commits should go into the `release` branch that will eventually be deployed to production. How would you handle this situation in Git?

### Answer

In this scenario, the goal is to **selectively move only specific commits from the `develop` branch to the `release` branch** without including all other commits. This situation often occurs when only certain features or fixes are ready for production while others are still under development.

There are two common approaches to achieve this.

---

### Option 1: Cherry-Pick Specific Commits

The most common and safest method is using **`git cherry-pick`**. This command allows you to apply specific commits from one branch to another.

This approach is widely used in release management when only selected fixes or features should be included in a release.

#### Step 1: Switch to the Release Branch

First, switch to the release branch or create it if it does not exist.

    git checkout release

or create a new release branch:

    git checkout -b release

---

#### Step 2: Identify the Required Commits

Use the following command to view commit history in the `develop` branch:

    git log develop

From the commit list, identify the **commit hashes of the 5 commits** that need to be included in the release.

---

#### Step 3: Cherry-Pick the Required Commits

Apply the selected commits to the release branch.

    git cherry-pick <commit-hash-1> <commit-hash-2> <commit-hash-3> <commit-hash-4> <commit-hash-5>

Git will apply these commits sequentially.

If conflicts occur, resolve them manually and continue the cherry-pick process.

---

#### Step 4: Push the Release Branch

After verifying the changes, push the release branch to the remote repository.

    git push origin release

This results in a **clean release branch containing only the required commits**.

---

### Option 2: Interactive Rebase

Another approach is using **interactive rebase** to create a new branch containing only the desired commits.

This method rewrites commit history and is typically used when creating a new branch based on selected commits.

---

#### Step 1: Create a New Branch from Develop

Create a new branch from the `develop` branch.

    git checkout -b release-from-develop develop

---

#### Step 2: Start Interactive Rebase

Run an interactive rebase for the last 50 commits.

    git rebase -i HEAD~50

An editor will open showing the commit list.

---

#### Step 3: Select the Desired Commits

In the editor:

- Keep `pick` for the 5 commits that should remain
- Remove or mark `drop` for the other commits

Save and close the editor.

Git will rewrite the branch history with only the selected commits.

---

#### Step 4: Push the Branch

After the rebase is completed, push the branch to the remote repository.

    git push origin release-from-develop

---

### Recommendation

In most production workflows:

- **Cherry-pick is the preferred approach** because it does not rewrite history and works safely on shared branches.
- **Interactive rebase is useful when creating a completely clean branch history**, but it should be used carefully because it rewrites commit history.

---

### Interview Summary

If only specific commits from the `develop` branch need to be included in a release branch, I would typically use `git cherry-pick` to selectively apply those commits to the release branch. This approach keeps the release branch clean and avoids rewriting commit history. Interactive rebase can also be used when creating a new branch with only selected commits, but cherry-pick is generally safer for collaborative environments.

### Question
A developer created an application module and made around 100 commits locally. Now the developer needs to push the changes to the remote `develop` branch as a single commit because the team does not want messy commit history in the `develop` branch. How would you handle this?

### Answer

When developers make many local commits during development, it can clutter the shared branch history. To maintain a clean and meaningful history in the `develop` branch, all local commits can be **squashed into a single commit before pushing**.

There are two common ways to achieve this.

---

### Method 1: Using Soft Reset (Simple and Common)

This method combines all local commits into a single commit by resetting the branch while keeping the changes staged.

#### Step 1: Ensure you are on the correct branch

If the developer is working directly on `develop`:

    git checkout develop

Or if development happened on a feature branch:

    git checkout feature-branch

---

#### Step 2: Reset commits while keeping changes staged

Run a soft reset against the remote `develop` branch:

    git reset --soft origin/develop

Explanation:

- `--soft` resets the commit history
- All code changes remain staged
- Git now treats all changes as if they were made at once

At this point, the 100 commits are effectively combined into staged changes.

---

#### Step 3: Create a single clean commit

Now create one meaningful commit representing the complete feature:

    git commit -m "Add application module"

This replaces the previous 100 commits with a single clean commit.

---

#### Step 4: Push the commit to the remote branch

Push the branch to the remote repository:

    git push origin develop

If the remote `develop` branch has new commits, first synchronize the branch:

    git pull --rebase origin develop
    git push origin develop

---

### Method 2: Using Interactive Rebase (More Control)

If you want to squash commits more selectively, interactive rebase can be used.

Start an interactive rebase for the last 100 commits:

    git rebase -i HEAD~100

An editor will open with the list of commits.

Keep the first commit as:

    pick

Change the remaining commits to:

    squash

or

    s

Save and exit the editor.

Git will combine all commits into a single commit and allow you to edit the final commit message.

After finishing the rebase, push the changes:

    git push origin develop

---

### Recommendation

For most workflows, the **soft reset method is simpler and faster** when you want to squash all commits into one. Interactive rebase is useful when you need finer control over which commits are combined.

---

### Interview Summary

If a developer has many local commits that should appear as a single commit in the `develop` branch, I would squash the commits before pushing. The simplest method is using `git reset --soft origin/develop`, which keeps all changes staged, then creating a single commit and pushing it to the remote branch. Interactive rebase can also be used when more control over commit squashing is needed.

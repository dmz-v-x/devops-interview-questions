### Question
You have made several commits on your feature branch but later realize that one of the earlier commits introduced a bug. How would you fix this without losing the other changes on your branch?

### Answer

When a bug is introduced in one of the earlier commits on a feature branch, the goal is to fix or undo that specific commit **without removing the other valid commits that came after it**.

There are two common approaches depending on whether the branch is **shared with others or still local/private**.

---

### Method 1: Using `git revert` (Safe for Shared Branches)

`git revert` creates a **new commit that undoes the changes made by a previous commit**, while keeping the rest of the commit history intact.

This approach is recommended when the branch has already been pushed or shared with other developers.

#### Step 1: Identify the commit that introduced the bug

View the commit history:

    git log

Locate the commit hash of the problematic commit.

---

#### Step 2: Revert the commit

    git revert <commit-hash>

Git will create a new commit that reverses the changes introduced by that commit.

If conflicts occur, resolve them manually and then commit the changes.

---

#### Advantages of Using Revert

- Safe for shared branches
- Does not rewrite commit history
- Maintains a complete audit trail

---

### Method 2: Using Interactive Rebase (For Local or Private Branches)

If the branch has not yet been shared with others, you can modify the earlier commit directly using **interactive rebase**.

This allows you to edit, remove, or fix specific commits.

---

#### Step 1: Start an interactive rebase

For example, if the buggy commit is within the last 5 commits:

    git rebase -i HEAD~5

Git will open an editor showing the list of recent commits.

---

#### Step 2: Choose how to modify the commit

In the editor you will see options such as:

- `pick` → keep the commit unchanged  
- `edit` → modify the commit  
- `drop` → remove the commit entirely  

Change the problematic commit from:

    pick

to

    edit

Save and close the editor.

---

#### Step 3: Fix the bug

Git will pause at the selected commit.

Make the necessary code fixes, then stage the changes:

    git add <file>

Amend the commit:

    git commit --amend

---

#### Step 4: Continue the rebase

    git rebase --continue

Git will replay the remaining commits on top of the corrected commit.

---

#### Advantages of Interactive Rebase

- Produces a clean commit history
- Allows fixing the original commit instead of adding extra commits
- Useful before pushing the branch

---

### Important Consideration

Interactive rebase **rewrites commit history**, so it should **not be used on branches that are already shared with other developers**.

---

### Interview Summary

If a bug is introduced in an earlier commit, I can either use `git revert` to safely undo the changes without rewriting history, which is ideal for shared branches, or use `git rebase -i` to edit or fix the commit directly when working on a local or private branch.

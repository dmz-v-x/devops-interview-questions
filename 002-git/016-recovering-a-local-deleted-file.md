### Question
You accidentally deleted a file from your local Git repository that you still need. How would you recover it?

### Answer

If a file is accidentally deleted from a local Git repository, the recovery method depends on whether the file was **committed, staged, or never tracked by Git**.

Git can recover files that were previously committed or tracked, but it cannot recover files that were never committed.

---

### Case 1: The File Was Tracked and Already Committed

If the file existed in the previous commit and was accidentally deleted from the working directory, it can be restored from the latest commit.

    git checkout -- path/to/file

Explanation:

- This command restores the file from the latest commit.
- The deleted file will reappear in the working directory.

This works as long as the file was previously committed to the repository.

---

### Case 2: The File Was Staged but Not Yet Committed

If the file was staged using `git add` but not yet committed, you can first unstage it and then restore the file.

Step 1: Unstage the file

    git reset HEAD path/to/file

Step 2: Restore the file from the last commit

    git checkout -- path/to/file

Explanation:

- `git reset HEAD` removes the file from the staging area.
- `git checkout --` restores the file from the last committed version.

---

### Case 3: The File Was Never Committed (Untracked File)

If the file was never committed to Git and was deleted from the working directory, Git cannot recover it.

In this case, recovery options include:

- restoring the file from a system backup
- retrieving it from an external source
- recreating the file manually

This is because Git only tracks files that have been committed to the repository.

---

### Interview Summary

If a file is accidentally deleted, I would recover it from the last commit using `git checkout -- path/to/file` if it was previously committed. If it was staged but not committed, I would first unstage it using `git reset HEAD` and then restore it. If the file was never committed, Git cannot recover it and it must be restored from a backup or recreated.

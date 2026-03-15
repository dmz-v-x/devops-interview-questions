### Question
You've been working on a feature branch for some time and want to share your progress with your team for review. How would you go about this?

### Answer

When working on a feature branch, it is common to share progress with teammates for feedback and code review before merging the changes into the main development branch. This is typically done by committing your changes, pushing the branch to the remote repository, and creating a pull request (or merge request).

---

### Step 1: Commit Your Work Locally

First, ensure all your changes are properly committed in your local repository.

    git add .
    git commit -m "Describe your progress"

This saves your work as a commit and prepares it to be shared with others.

---

### Step 2: Push the Feature Branch to the Remote Repository

If the feature branch does not yet exist on the remote repository, push it and set the upstream branch:

    git push -u origin feature-branch

Explanation:

- `origin` refers to the remote repository.
- `feature-branch` is the branch containing your work.
- The `-u` flag sets the upstream branch, allowing future pushes to be done simply with:

    git push

If the branch already exists remotely, you only need to run:

    git push

---

### Step 3: Create a Pull Request (PR) or Merge Request (MR)

After pushing the branch, go to your Git hosting platform such as:

- GitHub
- GitLab
- Bitbucket

Create a **Pull Request (PR)** or **Merge Request (MR)** from:

    feature-branch → main (or develop)

When creating the PR, include important details such as:

- A summary of the work completed
- Any remaining tasks
- Known issues or limitations
- Relevant screenshots or testing notes if applicable

Then assign reviewers from your team.

---

### Step 4: Encourage Code Review and Collaboration

Once the pull request is created:

- Team members review the code.
- They can comment on specific lines of code.
- They may approve the changes or request modifications.

If changes are requested, you can make updates and push additional commits to the same feature branch. The pull request will automatically update with the new commits.

---

### Interview Summary

To share progress on a feature branch, I would commit my changes locally, push the feature branch to the remote repository, create a pull request for review, and collaborate with the team through code reviews and updates until the changes are approved for merging.

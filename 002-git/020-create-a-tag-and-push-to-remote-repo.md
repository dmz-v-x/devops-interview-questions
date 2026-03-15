### Question
How do you create a Git tag and push it to the remote repository?

### Answer

Git tags are used to **mark specific points in a repository's history**, typically to represent software releases such as `v1.0.0`, `v2.1.3`, etc. Tags make it easy to reference important versions of the codebase.

There are two main types of tags in Git:

- **Lightweight tags**
- **Annotated tags**

---

### Create a Lightweight Tag

A lightweight tag is simply a pointer to a specific commit. It does not include additional metadata such as the tagger name, message, or date.

    git tag <tag-name>

Example:

    git tag v1.0.0

This creates a tag pointing to the current commit.

---

### Create an Annotated Tag (Recommended)

Annotated tags are preferred for releases because they include additional metadata such as:

- tag message
- author
- timestamp

Command:

    git tag -a <tag-name> -m "Tagging version <tag-name>"

Example:

    git tag -a v1.0.0 -m "Release version 1.0.0"

This creates a more informative tag suitable for production releases.

---

### Push a Specific Tag to the Remote Repository

After creating a tag locally, it must be pushed to the remote repository.

    git push origin <tag-name>

Example:

    git push origin v1.0.0

This pushes the specific tag to the remote repository.

---

### Push All Local Tags

If multiple tags exist locally and you want to push all of them:

    git push origin --tags

This pushes all local tags to the remote repository.

---

### Verify Tags

To list all tags in the repository:

    git tag

To view details of an annotated tag:

    git show <tag-name>

Example:

    git show v1.0.0

---

### Best Practice

Annotated tags are generally recommended for release management because they provide more context and metadata for each version.

---

### Interview Summary

To create a Git tag, I use `git tag -a <tag-name> -m "message"` for an annotated tag and then push it to the remote repository using `git push origin <tag-name>`. Tags are commonly used to mark release versions so that specific code states can be referenced easily.

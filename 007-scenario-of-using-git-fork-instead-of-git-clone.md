### Q: Explain a scenario where you used git fork instead of git clone. Why was forking necessary?

**Answer:**

I used **git fork** when contributing to a repository owned by an organization where I did not have direct write access.

In this case, the repository contained Helm charts used for Kubernetes deployments, and I needed to fix a bug in the Helm values configuration. Since the repository belonged to an organization and write access was restricted, I could not push changes directly to the main repository.

To solve this, I used the **Fork** option on GitHub to create a copy of the repository under my own GitHub account. This gave me full write access to my own version of the repository while keeping a connection to the original (upstream) project.

After forking:

- I cloned my fork to my local machine:

      git clone https://github.com/my-username/devops-helm-project.git

- I created a new branch, fixed the Helm chart issue, and committed the changes.
- I pushed the branch to my fork:

      git push origin bugfix-helm-values

- Finally, I opened a **Pull Request** from my fork to the original organization repository so the maintainers could review and merge the fix.

Forking was necessary because simply cloning the upstream repository would not allow me to push changes or raise a pull request due to missing write permissions.

> **Depth addition:** Forking creates an independent remote repository that you control, which is a requirement for contributing to repositories where you only have read access.

---

### Summary (Interview-Friendly Line)

I used git fork because the repository was owned by an organization and I lacked write access. Forking allowed me to make changes in my own repository and contribute them back safely through a pull request.

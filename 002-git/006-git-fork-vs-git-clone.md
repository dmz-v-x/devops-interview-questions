### Q: What is the difference between `git fork` and `git clone`, and when would you use each?

**Answer:**

`git fork` and `git clone` are related but serve very different purposes. They operate at different levels of the Git workflow.

---

### Git Fork  
A **fork** creates a copy of a repository at the **platform level** (such as GitHub, GitLab, or Bitbucket) under your own account.

Key points:
- Creates a **separate repository** in your account  
- Used when you **do not have write access** to the original repository  
- Common in **open-source contributions** and large team projects  
- Changes are proposed back using **Pull Requests (PRs)**  

Typical workflow:
1. Fork the original repository  
2. Clone your fork to your local machine  
3. Make changes and push them to your fork  
4. Create a pull request to the original repository  

> **Depth addition:** Forking creates a permanent, independent copy that you fully control, while still allowing collaboration with the upstream project.

---

### Git Clone  
`git clone` creates a **local copy** of a repository on your machine.

Key points:
- Copies a repository from a remote source to your local system  
- Used for **development and experimentation**  
- Works with both **your own repositories** and **others’ repositories**  
- Requires no special permissions to clone (only read access)  

> **Important clarification:** Cloning alone does **not** give you permission to push changes back to the original repository unless you have write access.

---

### Fork vs Clone (Key Difference)

- **Fork** → Platform-level action (GitHub/GitLab), creates a new remote repository  
- **Clone** → Local-level action, creates a working copy on your machine  

> **Interview-friendly line:**  
Fork is about ownership and permissions, while clone is about getting the code locally.

---

### When to use each

- Use **fork** when:
  - You don’t have write access  
  - You want to contribute to open-source  
  - You need an independent copy under your account  

- Use **clone** when:
  - You want to work on a repository locally  
  - You already have write access  
  - You are cloning your fork or your own repository  

---

### Summary (Interview-Friendly Line)  
Fork creates a separate copy of a repository in your GitHub account for independent contribution, while clone downloads a repository to your local machine for development. Fork handles permission and ownership; clone handles local access.

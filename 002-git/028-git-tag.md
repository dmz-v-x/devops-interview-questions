### Question  
Have you ever used Git tags? If yes, why?

---

### Answer  

Yes, I have used **Git tags** primarily to mark **release versions** of applications.

---

### 1. Why I Used Git Tags

- To identify which commit corresponds to a **production deployment**  
- To make:
  - Rollbacks easier  
  - Auditing changes simpler  

---

### 2. Real-World Usage

- In one of my projects:
  - Every stable build (after CI/CD success) was tagged  

---

#### Example:

```
v1.0.3
```

---

- Tags were used by:
  - Jenkins pipelines  
- Deployment names included tag versions  
- Ensured clear visibility of:
  - What version is running in production  

---

### 3. Annotated Tags (Used in Practice)

```bash
git tag -a v1.0.3 -m "Release version 1.0.3 with critical bug fixes"
git push origin v1.0.3
```

---

#### Why annotated tags?

- Include metadata:
  - Author  
  - Date  
  - Message  
- Better for production releases  

---

### 4. Why Git Tags Are Useful

| Use Case              | Description                                              |
| -------------------- | -------------------------------------------------------- |
| Marking releases     | Identify stable versions                                 |
| Rollback support     | Easily revert to a known working state                   |
| CI/CD integration    | Trigger builds or deployments based on tags              |
| Version tracking     | Maintain consistent release history                      |

---

### 5. Key Takeaways

- Tags act like **bookmarks for important commits**  
- Essential for:
  - Release management  
  - Version control  
  - Deployment tracking  

---

### 6. Interview-Ready Summary

“Yes, I’ve used Git tags to mark release versions in production. We tagged stable builds after CI/CD validation, which helped us track deployments, perform rollbacks, and maintain version consistency. I typically used annotated tags to include context like release notes, and these tags were integrated with our Jenkins pipeline for versioned deployments.”

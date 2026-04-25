### Question  
Explain a recent challenge you faced with Git and how you addressed it.

---

### Answer  

---

### 1. Problem Statement

At an organization level, multiple teams were using **different Git workflows**, which led to:

- CI pipelines failing due to missing expected branches (`main`, `release`)  
- Teams rebasing public branches → breaking others’ work  
- Frequent merge conflicts in shared environments  
- Confusion around which branch was production-ready  
- Delays in releases  

---

### 2. Step 1: Analyze the Current State

- Audited repositories using:
  - GitHub/GitLab APIs  

- Identified:
  - Different branching strategies  
  - Inconsistent naming conventions  
  - Lack of governance  

---

### 3. Step 2: Design a Unified Strategy

Proposed a **trunk-based development model**:

---

#### Branch Structure:

- `main`  
  - Always **production-ready**  

- `release/x.y`  
  - Used for:
    - Stabilization  
    - Hotfixes  

- `feature/*`  
  - Short-lived branches  
  - Must be rebased before merge  

---

#### Rules Defined:

- No rebasing of public/shared branches  
- Mandatory Pull Requests  
- Enforced code reviews  
- CI must pass before merge  

---

### 4. Step 3: Rollout (Tooling + Education)

---

#### Tooling:

- Created **starter repo templates**  
- Standardized:
  - Branch structure  
  - CI/CD pipelines  

---

#### Automation:

- Configured:
  - Branch protection rules  
  - PR requirements  
  - GitHub Actions  

---

#### Enablement:

- Conducted:
  - Onboarding sessions  
- Created:
  - Lightweight Git handbook  

---

### 5. Step 4: Iterate with Feedback

- Collected feedback from:
  - Developers  
  - QA teams  
  - Platform teams  

---

#### Adjustments:

- Allowed temporary exceptions during migration  
- Fine-tuned workflows for real-world usage  

---

### 6. Outcome

- Reduced merge conflicts  
- Improved CI pipeline stability  
- Clear production-ready branch (`main`)  
- Faster and more predictable releases  
- Better collaboration across teams  

---

### 7. Key Takeaways

- Standardization is critical at scale  
- Avoid rebasing shared branches  
- Automate enforcement (CI + policies)  
- Combine process + education  

---

### 8. Interview-Ready Summary

“At an organizational level, inconsistent Git practices caused CI failures, merge conflicts, and release delays. I addressed this by auditing repositories, designing a unified trunk-based strategy, and enforcing it through templates, automation, and branch protection rules. I also conducted training sessions and iterated based on feedback, which significantly improved stability, collaboration, and release efficiency.”

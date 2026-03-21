### Question  
Different types of deployment strategies in Kubernetes?

---

### Answer  

### 1. Recreate Deployment  

- Terminates all old Pods → then starts new Pods  

Spec:

    spec:
      strategy:
        type: Recreate

Pros:

- Simple  
- Clean environment  

Cons:

- Causes downtime  

Use case:

- Non-critical apps  
- Maintenance scenarios  

---

### 2. Rolling Update (Default)  

- Gradually replaces old Pods with new ones  

Spec:

    spec:
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxSurge: 1
          maxUnavailable: 1

Pros:

- Zero downtime  
- Safe and controlled rollout  

Cons:

- Slower  
- Temporary version mix  

Use case:

- Most production applications  

---

### 3. Blue-Green Deployment  

- Two environments:

  - Blue → current version  
  - Green → new version  

- Switch traffic after testing  

Pros:

- Instant rollback  
- Near-zero downtime  

Cons:

- Requires double resources  

Use case:

- Critical systems  

Implementation:

- Switch via Service or Ingress  

---

### 4. Canary Deployment  

- Deploy new version to small % of users  
- Gradually increase traffic  

Pros:

- Reduced risk  
- Real-world testing  

Cons:

- More complex  

Use case:

- Feature rollout  
- Risk mitigation  

Implementation:

- Ingress / Service Mesh  

---

### 5. A/B Testing (Advanced Canary)  

- Route traffic based on:

  - User attributes  
  - Headers  
  - Regions  

Pros:

- Targeted experimentation  

Cons:

- Requires advanced routing  

Use case:

- Feature testing  

---

### 6. Summary  

| Strategy       | Downtime | Rollback    | Resources | Use Case          |
|----------------|----------|-------------|-----------|-------------------|
| Recreate       | Yes      | Simple      | Normal    | Non-critical apps |
| Rolling Update | No       | Gradual     | Normal    | Default strategy  |
| Blue-Green     | No       | Instant     | High      | Critical apps     |
| Canary         | No       | Gradual     | Normal    | Risk mitigation   |
| A/B Testing    | No       | Conditional | Normal    | Feature targeting |

---

### 7. Key Insight  

- Default = **Rolling Update**  
- Advanced strategies = **traffic control + risk management**  

---

### Interview Summary  

Kubernetes supports multiple deployment strategies. Rolling updates are the default and provide zero downtime. Recreate is simple but causes downtime. Blue-green and canary deployments offer safer rollouts with better rollback capabilities, while A/B testing enables targeted feature experimentation. Choosing the right strategy depends on application criticality and risk tolerance.

### Question
What is the difference between Continuous Delivery and Continuous Deployment?

### Answer

Continuous Delivery and Continuous Deployment are DevOps practices designed to accelerate software releases by automating the build, testing, and deployment processes. The key difference lies in **whether production deployment requires manual approval**.

---

### Continuous Delivery

Continuous Delivery means that every code change automatically goes through the following stages:

- build
- automated testing
- validation

After passing these steps, the application is **ready to be deployed to production at any time**, but the final deployment step requires manual approval.

Key characteristics:

- Code is always in a deployable state
- Deployment to production is controlled by a human decision
- Teams maintain control over release timing

Example:

A developer merges code into the main branch. The CI/CD pipeline builds and tests the application. The artifact is ready, and a release manager manually approves deployment to production.

Advantages:

- Safer releases
- Opportunity for manual checks
- Suitable for systems requiring strict release control

---

### Continuous Deployment

Continuous Deployment takes automation one step further.

Every change that successfully passes automated tests is **automatically deployed to production without manual approval**.

Key characteristics:

- Fully automated pipeline
- No manual intervention
- Very fast feedback from real users

Example:

A developer merges code into the main branch. The CI/CD pipeline builds, tests, and automatically deploys the change to production within minutes.

Advantages:

- Faster delivery of new features
- Immediate feedback from users
- Highly efficient development cycle

Limitations:

- Requires very strong automated testing
- Requires reliable monitoring and rollback mechanisms

---

### Key Difference

| Feature | Continuous Delivery | Continuous Deployment |
|------|---------------------|----------------------|
| Deployment to production | Manual approval required | Fully automated |
| Automation level | High | Very high |
| Risk level | Lower | Higher if tests fail |
| Release control | Controlled by team | Automated pipeline |

---

### Interview Summary

Continuous Delivery ensures that code is always ready for production but requires manual approval for deployment, while Continuous Deployment automatically deploys every successful change to production without manual intervention.

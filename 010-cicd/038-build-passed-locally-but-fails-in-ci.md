### Question  
Build Passed Locally but Fails in CI — How Will You Troubleshoot?

---

### Answer  

This issue usually occurs due to differences between the local development environment and the CI environment — such as configuration, dependencies, or runtime versions.

---

### Step-by-Step Troubleshooting Approach

---

### 1. Check the Error Logs in CI

- Start with:
  - CI build logs  

- Identify the type of failure:
  - Compilation error  
  - Test failure  
  - Dependency issue  
  - Permission issue  

---

### 2. Reproduce in a CI-Like Environment

- Use:
  - Clean Docker container  
  - Fresh VM  

- Match CI environment as closely as possible:

```bash
docker run -it --rm openjdk:17 bash
# Run build commands inside
```

---

### 3. Compare Local vs CI Environment

Check for differences in:

- OS version  
- Language/runtime versions (Java, Node, Python)  
- Build tools (Maven, Gradle, npm)  
- Environment variables  
- Resource limits (CPU, memory)  

---

### 4. Verify Secrets and Credentials

CI failures often occur due to missing:

- Git credentials  
- API tokens  
- Config files:
  - `.npmrc`  
  - `.pypirc`  

Ensure:

- Secrets are properly injected via CI  
- Access permissions are correct  

---

### 5. Check Dependency Issues

- Local machine may use cached dependencies:

```text
~/.m2/repository
```

- CI runs in a clean environment  

- Validate dependencies:

```bash
mvn dependency:tree
npm ls
```

---

### 6. Check File and Path Issues

- Common issues:
  - Case sensitivity (Linux vs Windows)  
  - Missing files  
  - Incorrect paths  
  - File permissions  

---

### Example Scenario

---

#### Error in CI

```text
error: package javax.annotation does not exist
```

---

#### Root Cause

- Local:
  - Java 8  

- CI:
  - Java 11  

- Issue:
  - Package not included by default in Java 11  

---

#### Fix

- Add dependency explicitly in `pom.xml`  
- Align JDK version between local and CI  

---

### Key Takeaways

- CI failures are usually due to:
  - Environment mismatch  
  - Missing dependencies  
  - Misconfigured secrets  

- Always:
  - Reproduce in clean environment  
  - Standardize versions  

---

### Interview-Ready Summary

“When a build passes locally but fails in CI, I start by analyzing CI logs to identify the error type. Then I reproduce the issue in a clean environment like a Docker container to mimic CI. I compare local and CI environments for differences in OS, tool versions, and environment variables. I also verify secrets, dependency resolution, and file paths. In most cases, the issue comes down to environment mismatch or missing dependencies, which I fix by standardizing configurations and making dependencies explicit.”

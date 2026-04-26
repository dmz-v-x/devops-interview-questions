### Question  
Talk about 5 build targets that you use on a day-to-day basis in Maven.

---

### Answer  

Maven uses build lifecycle phases (also called build targets) to automate compilation, testing, packaging, and deployment of applications. These phases are executed using commands like:

```bash
mvn <goal>
```

---

### 1. mvn clean

---

#### Purpose

- Deletes the `target/` directory  
- Removes previous build artifacts  

---

#### When I Use It

- Before a fresh build  
- To avoid conflicts from old compiled files  

---

### 2. mvn compile

---

#### Purpose

- Compiles source code from:

```text
src/main/java
```

---

#### When I Use It

- To verify:
  - No compilation errors  

---

### 3. mvn test

---

#### Purpose

- Runs unit tests  

- Common frameworks:
  - JUnit  
  - TestNG  

---

#### When I Use It

- During development  
- In CI pipelines to ensure stability  

---

### 4. mvn package

---

#### Purpose

- Packages application into:
  - `.jar`  
  - `.war`  

---

#### When I Use It

- When build is stable  
- To generate deployable artifact  

---

### 5. mvn install

---

#### Purpose

- Installs artifact into local repository:

```text
~/.m2/repository
```

---

#### When I Use It

- When working with:
  - Shared libraries  
  - Multi-module projects  

- So other projects can use the artifact locally  

---

### Key Takeaways

- Maven lifecycle automates:
  - Build → Test → Package → Install  

- These commands are commonly used in:
  - Development  
  - CI/CD pipelines  

---

### Interview-Ready Summary

“I commonly use mvn clean to remove old build artifacts, mvn compile to check for compilation errors, mvn test to run unit tests, mvn package to create deployable artifacts like JARs or WARs, and mvn install to place the artifact in the local Maven repository for reuse across projects. These commands form the core of my daily Maven workflow and are also used in CI/CD pipelines.”

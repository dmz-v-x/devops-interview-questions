### Question  
How do you configure Artifactory for your application in Maven?

---

### Answer  

To integrate Maven with Artifactory, we configure:

1. Authentication credentials in `settings.xml`  
2. Repository endpoints in `pom.xml`  

This allows Maven to:

- Pull dependencies from Artifactory  
- Push build artifacts to Artifactory  

---

### Step 1: Configure Credentials (settings.xml)

Location:

```text
~/.m2/settings.xml
```

Add server credentials:

```xml
<settings>
  <servers>
    <server>
      <id>artifactory-repo</id>
      <username>your-username</username>
      <password>your-password</password>
    </server>
  </servers>
</settings>
```

- `id` must match the repository ID used in `pom.xml`  

---

### Step 2: Configure Repositories (pom.xml)

---

#### For Downloading Dependencies

```xml
<repositories>
  <repository>
    <id>artifactory-repo</id>
    <url>https://your-artifactory-url/artifactory/libs-release</url>
  </repository>
</repositories>
```

---

#### For Deploying Artifacts

```xml
<distributionManagement>
  <repository>
    <id>artifactory-repo</id>
    <url>https://your-artifactory-url/artifactory/libs-release-local</url>
  </repository>
  <snapshotRepository>
    <id>artifactory-repo</id>
    <url>https://your-artifactory-url/artifactory/libs-snapshot-local</url>
  </snapshotRepository>
</distributionManagement>
```

---

### Step 3: Deploy Artifact

```bash
mvn clean deploy
```

---

### What This Achieves

- Pull dependencies from Artifactory (via `<repositories>`)  
- Push artifacts (`.jar`, `.war`) to Artifactory  
- Support:
  - Release repositories  
  - Snapshot repositories  

---

### Key Takeaways

- `settings.xml`:
  - Stores credentials  

- `pom.xml`:
  - Defines repository locations  

- `mvn deploy`:
  - Publishes artifacts  

---

### Interview-Ready Summary

“To configure Artifactory with Maven, I add authentication credentials in settings.xml and define repository endpoints in pom.xml using repositories and distributionManagement. This setup allows Maven to pull dependencies from Artifactory and push build artifacts using mvn clean deploy. It also supports both snapshot and release repositories for proper artifact versioning.”

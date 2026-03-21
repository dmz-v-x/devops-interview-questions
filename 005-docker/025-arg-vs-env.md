### Question  
What are `ARG` and `ENV` in a Dockerfile, and how do they differ?

---

### Answer  

### 1. ARG (Build-Time Variable)  

#### Definition  

`ARG` is used to define variables that are available **only during the image build process**.

- Not available in the running container  
- Used for build customization  

---

#### Example  

    FROM ubuntu:20.04

    ARG APP_VERSION=1.0
    RUN echo "Building version: $APP_VERSION"

---

#### Pass Value at Build Time  

    docker build --build-arg APP_VERSION=2.0 -t myapp:2.0 .

---

#### Key Points  

- Scope: Build-time only  
- Not persisted in final container  
- Useful for:
  - Versioning  
  - Conditional builds  

---

### 2. ENV (Runtime Variable)  

#### Definition  

`ENV` sets environment variables that are available **inside the running container**.

- Persist in the image  
- Accessible to applications  

---

#### Example  

    FROM ubuntu:20.04

    ENV APP_ENV=production
    CMD ["sh", "-c", "echo Running in $APP_ENV mode"]

---

#### Override at Runtime  

    docker run -e APP_ENV=staging myapp

---

#### Key Points  

- Scope: Runtime (inside container)  
- Persisted in image  
- Used for:
  - App configuration  
  - Environment settings  

---

### 3. ARG vs ENV (Comparison Table)  

| Feature | ARG | ENV |
|---|---|---|
| Scope | Build-time only | Runtime |
| Available in container | ❌ No | ✅ Yes |
| Persist in image | ❌ No | ✅ Yes |
| Override | `--build-arg` | `-e` |
| Use case | Versions, build configs | App configs |

---

### 4. Using ARG + ENV Together  

You can pass ARG → ENV:

---

#### Example  

    FROM ubuntu:20.04

    ARG VERSION=1.0
    ENV APP_VERSION=$VERSION

---

- `ARG` used during build  
- `ENV` persists into container  

---

### 5. Key Concept  

- `ARG` → build-time customization  
- `ENV` → runtime configuration  

---

### 6. Real-World Example  

---

#### Build  

    docker build --build-arg NODE_VERSION=18 -t myapp .

---

#### Dockerfile  

    ARG NODE_VERSION
    ENV APP_ENV=production

---

- NODE_VERSION → used to install dependencies  
- APP_ENV → used by application  

---

### 7. Tricky Interview Questions  

---

Can ARG be accessed inside container?  

- ❌ No (unless passed to ENV)  

---

Can ENV be overridden?  

- ✅ Yes (`docker run -e`)  

---

Which is safer for secrets?  

- ❌ Neither (use secret managers)  

---

Does ARG exist after build?  

- ❌ No  

---

### Interview Summary  

`ARG` is used for build-time variables and is not available in the running container, while `ENV` defines environment variables that persist inside the container at runtime. Typically, `ARG` is used for build configurations like versions, and `ENV` is used for application settings like environment modes.

### Question  
What is the difference between `ENTRYPOINT` and `CMD` in Docker?

---

### Answer  

### 1. Core Difference  

| Feature | ENTRYPOINT | CMD |
|---|---|---|
| Purpose | Defines the main executable | Provides default arguments |
| Override | Only via `--entrypoint` | Easily overridden |
| Role | Fixed command | Flexible defaults |
| Usage | Enforce a command | Provide default behavior |

---

### 2. CMD (Default Command)  

#### Definition  

`CMD` specifies the **default command or arguments** for a container.

---

#### Example  

    FROM ubuntu
    CMD ["echo", "Hello from CMD"]

---

#### Behavior  

Run:

    docker run my-image

Output:

    Hello from CMD

---

#### Override CMD  

    docker run my-image echo Goodbye

Output:

    Goodbye

---

✅ CMD is **easily replaceable**  

---

### 3. ENTRYPOINT (Main Command)  

#### Definition  

`ENTRYPOINT` defines the **main executable** that always runs.

---

#### Example  

    FROM ubuntu
    ENTRYPOINT ["echo"]

---

#### Behavior  

Run:

    docker run my-image Hello

Output:

    Hello

---

- `echo` is fixed  
- Arguments can change  

---

### 4. ENTRYPOINT + CMD Together  

Best practice: combine both

---

#### Example  

    FROM ubuntu
    ENTRYPOINT ["echo"]
    CMD ["Hello from CMD"]

---

#### Behavior  

Run:

    docker run my-image

Output:

    Hello from CMD

---

#### Override CMD  

    docker run my-image Goodbye

Output:

    Goodbye

---

#### Override ENTRYPOINT  

    docker run --entrypoint ls my-image

Output:

    (runs ls command)

---

### 5. Key Concept  

- ENTRYPOINT = **fixed command**  
- CMD = **default arguments**

---

### 6. Mental Model  

Think of:

    ENTRYPOINT = program  
    CMD = parameters  

---

Example:

    ENTRYPOINT ["node"]
    CMD ["app.js"]

---

Run:

    docker run my-image server.js

→ Executes:

    node server.js

---

### 7. Best Practices  

---

#### Use ENTRYPOINT  

- When container should always run a specific program  

---

#### Use CMD  

- When you want flexibility  

---

#### Use Both Together  

- ENTRYPOINT → fixed executable  
- CMD → default arguments  

---

### 8. Tricky Interview Questions  

---

Does CMD run if ENTRYPOINT exists?  

- ✅ Yes (as arguments)  

---

Can CMD override ENTRYPOINT?  

- ❌ No  

---

Which one is preferred for scripts?  

- ENTRYPOINT  

---

Which one is easier to override?  

- CMD  

---

### Interview Summary  

`ENTRYPOINT` defines the fixed main command of a container, while `CMD` provides default arguments that can be overridden. Together, they allow you to create flexible yet controlled container behavior, where ENTRYPOINT ensures consistency and CMD allows customization.

### Question  
What is the difference between CMD and ENTRYPOINT in a Dockerfile?

---

### Answer  

---

### 1. Core Difference

- `ENTRYPOINT`:
  - Defines the **fixed command** that always runs  

- `CMD`:
  - Provides **default arguments or command**  
  - Can be overridden at runtime  

---

### 2. Conceptual Understanding

- `ENTRYPOINT` → “What should always run”  
- `CMD` → “Default values for that command”  

---

### 3. Detailed Comparison

| Aspect              | CMD                                   | ENTRYPOINT                              |
|---------------------|----------------------------------------|------------------------------------------|
| **Purpose**         | Default command/arguments              | Fixed executable                         |
| **Override**        | Easily overridden                      | Not overridden (unless `--entrypoint`)   |
| **Flexibility**     | Flexible                               | Strict                                   |
| **Use case**        | Provide defaults                       | Enforce main container behavior          |

---

### 4. Example — CMD

```dockerfile
FROM ubuntu
CMD ["echo", "Hello from CMD"]
```

Run:

```bash
docker run myimage
```

Output:
```
Hello from CMD
```

Override:

```bash
docker run myimage echo "Overridden"
```

Output:
```
Overridden
```

---

### 5. Example — ENTRYPOINT

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
```

Run:

```bash
docker run myimage Hello from ENTRYPOINT
```

Output:
```
Hello from ENTRYPOINT
```

- Cannot override command directly  
- Requires:

```bash
docker run --entrypoint <new_command> myimage
```

---

### 6. Using CMD + ENTRYPOINT Together

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello from CMD"]
```

Run:

```bash
docker run myimage
```

Output:
```
Hello from CMD
```

Override arguments:

```bash
docker run myimage Custom message
```

Output:
```
Custom message
```

- Final execution:
  - `ENTRYPOINT + CMD`  
  - `echo Hello from CMD`  

---

### 7. Key Takeaways

- `ENTRYPOINT`:
  - Defines main command  
  - Always executed  

- `CMD`:
  - Provides default arguments  
  - Easily overridden  

- Together:
  - `CMD` acts as arguments to `ENTRYPOINT`  

---

### 8. Interview-Ready Summary

“CMD and ENTRYPOINT both define what runs inside a container. ENTRYPOINT specifies the fixed command that always executes, while CMD provides default arguments that can be overridden at runtime. When used together, ENTRYPOINT defines the executable and CMD supplies its default arguments, making containers both predictable and flexible.”

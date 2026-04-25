### Question  
What are **ours** and **theirs** strategies in Git merges? How and when are they used?

---

### Answer  

---

### 1. Overview

- **ours** → Keeps changes from the **current branch**  
- **theirs** → Keeps changes from the **incoming branch**  

---

### 2. `ours` Strategy (Merge Strategy)

- Built-in **merge strategy**  

---

#### Usage:

```bash
git merge -s ours feature-branch
```

---

#### Behavior:

- Ignores all changes from the incoming branch  
- Keeps current branch content entirely  

---

#### Use Cases:

- You want to:
  - Mark branch as merged  
  - Ignore its changes  
- Useful for:
  - Closing feature branches  
  - Skipping unwanted changes  

---

### 3. `theirs` Strategy (Conflict Resolution)

- Not a full merge strategy like `ours`  
- Used during **conflict resolution**  

---

#### Usage:

```bash
git checkout --theirs conflicted_file.txt
git add conflicted_file.txt
```

---

#### Behavior:

- Replaces your version with incoming branch version  

---

#### Use Cases:

- You want:
  - Incoming branch changes to override yours  
- Useful when:
  - You trust the other branch more  
  - You want quick conflict resolution  

---

### 4. Important Note

- `ours` = full merge strategy  
- `theirs` = conflict-level resolution (not `-s theirs`)  

---

### 5. Comparison Table

| Strategy  | Behavior                                  | Use When...                                             |
|-----------|--------------------------------------------|---------------------------------------------------------|
| `ours`    | Keeps **current branch’s** content          | Ignore incoming branch changes                          |
| `theirs`  | Keeps **incoming branch’s** content         | Override local changes during conflict resolution       |

---

### 6. Example Scenario

---

#### Conflict:

```text
<<<<<<< HEAD
Version A
=======
Version B
>>>>>>> feature
```

---

#### Resolve using theirs:

```bash
git checkout --theirs file.txt
git add file.txt
```

→ Keeps **Version B**

---

### 7. Key Takeaways

- `ours`:
  - Used at merge level  
  - Keeps current branch  

- `theirs`:
  - Used at conflict level  
  - Keeps incoming branch  

---

### 8. Interview-Ready Summary

“In Git, the ‘ours’ strategy is a merge strategy that keeps the current branch’s content and ignores incoming changes, typically used to mark a branch as merged without applying its changes. ‘Theirs’ is not a standalone merge strategy but is used during conflict resolution to accept the incoming branch’s version of a file. These strategies help control how conflicts are resolved during merges.”

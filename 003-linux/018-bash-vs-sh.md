### Question
What is the difference between `bash` and `sh`?

### Answer

`bash` and `sh` are Unix/Linux command-line shells used for executing commands and writing shell scripts. Although they are related, they differ in terms of **features, portability, and compatibility**.

---

### What is `sh`?

`sh` stands for **Bourne Shell**.

- It is the **original Unix shell**, written by **Stephen Bourne**.
- It is typically used for **basic shell scripting and system scripts**.
- On modern Linux systems, `sh` is often a **symbolic link to another shell** such as `bash` or `dash` (a lightweight shell).

Example command:

```
sh script.sh
```

This executes the script using the **Bourne shell or a compatible shell**.

---

### What is `bash`?

`bash` stands for **Bourne Again Shell**.

- It is an **enhanced and improved version of `sh`**.
- It includes many additional features beyond the original Bourne shell.
- It is the **default shell in most Linux distributions**.
- It supports advanced scripting features such as:
  - arrays
  - arithmetic operations
  - string manipulation
  - improved command history
  - better interactive features

Example command:

```
bash script.sh
```

This runs the script using the **Bash interpreter**.

---

### Key Differences

| Feature | `sh` | `bash` |
|------|------|------|
| Full Name | Bourne Shell | Bourne Again Shell |
| Default Shell | Older systems with minimal features | Default shell in most Linux distributions |
| Scripting Features | Basic scripting capabilities | Advanced features such as arrays and functions |
| Portability | Highly portable across Unix systems | Less portable due to bash-specific features |
| Command History | Limited support | Full command history support |
| Prompt Customization | Minimal customization | Advanced prompt customization |
| Interactive Use | Basic functionality | Advanced features like tab completion and job control |

---

### Examples of Differences

#### Arrays (Supported in Bash Only)

Example in `bash`:

```
arr=(one two three)
echo ${arr[1]}
```

Output:

```
two
```

Arrays are **not supported in `sh`**.

---

#### Arithmetic Operations

In `bash`:

```
a=5
b=$((a + 3))
echo $b
```

Output:

```
8
```

In `sh`, arithmetic is typically done using `expr`:

```
b=`expr $a + 3`
```

---

#### String Manipulation

Example in `bash`:

```
str="hello world"
echo ${str^}
```

Output:

```
HELLO WORLD
```

This type of string manipulation **is not available in `sh`**.

---

### When to Use Each Shell

Use `sh` when:

- Writing **portable scripts** that must work across many Unix/Linux systems.
- Creating **simple scripts** with minimal dependencies.
- Writing **system initialization scripts** where portability matters.

Use `bash` when:

- Writing Linux-specific scripts.
- Using **advanced scripting features** like arrays and complex logic.
- Working interactively in a shell with enhanced features.

---

### How to Check Which Shell You Are Using

To check your login shell:

```
echo $SHELL
```

To see which shell is executing the current script:

```
echo $0
```

---

### Tricky Interview Questions

Can a bash script run with `sh`?

Yes, **if it only uses commands compatible with `sh`**.  
However, scripts that use **bash-specific features will fail** when executed with `sh`.

---

Why are many system scripts written in `sh`?

Because `sh` is **more portable and compatible across different Unix systems**.

---

How can you explicitly run a script with Bash even if `sh` is the default?

Use a **shebang line** at the top of the script:

```
#!/bin/bash
```

This ensures the script always runs using the Bash interpreter.

---

How can you check if `/bin/sh` is a symlink to Bash?

Run:

```
ls -l /bin/sh
```

Example output:

```
/bin/sh -> /bin/bash
```

This indicates that `sh` is linked to the Bash shell.

---

### Interview Summary

`sh` (Bourne Shell) is the original Unix shell designed for basic scripting and high portability, while `bash` (Bourne Again Shell) is an enhanced version that includes advanced scripting capabilities, better interactive features, and is the default shell in most modern Linux distributions.

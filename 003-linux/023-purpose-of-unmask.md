### Question
What is the purpose of the `umask` command?

### Answer

The `umask` command in Linux defines the **default permissions for newly created files and directories**.  
`umask` stands for **User File Creation Mask**, and it works by **removing permission bits from the system’s default permissions** when a new file or directory is created.

Instead of directly setting permissions, `umask` **subtracts permissions** from predefined defaults to determine the final permissions of new files and directories.

---

### What is `umask`?

`umask` (User File Creation Mask):

- Controls the **default permissions** assigned to new files and directories.
- Defines which permissions should **not be granted** by default.
- Ensures files are not created with overly permissive access.

It essentially **subtracts permissions from the system default** during file creation.

---

### Why is `umask` Important?

`umask` plays a key role in system security and access control.

Security benefits include:

- Restricting default access to newly created files
- Preventing files from being **world-readable or writable**
- Supporting the **principle of least privilege**, where users only get the minimum required permissions

Without `umask`, files could be created with overly permissive access, which could expose sensitive data.

---

### Default Permissions

Linux assigns default permissions before applying the `umask`.

| Object | Default Permission |
|------|------------------|
| Files | `666` (read & write for owner, group, others) |
| Directories | `777` (read, write, execute for owner, group, others) |

The `umask` value **removes bits from these defaults**.

---

### How `umask` Works (Formula)

The final permissions are calculated using the formula:

```
Default permissions - umask = actual permissions
```

Example 1:

```
umask = 022
```

File:

```
666 - 022 = 644
rw-r--r--
```

Directory:

```
777 - 022 = 755
rwxr-xr-x
```

Example 2:

```
umask = 077
```

File:

```
666 - 077 = 600
rw-------
```

Directory:

```
777 - 077 = 700
rwx------
```

This means only the **owner has access**, making it useful for sensitive files.

---

### Viewing the Current `umask`

To see the current `umask` value:

```
umask
```

Example output:

```
0022
```

To display it in symbolic format:

```
umask -S
```

Example output:

```
u=rwx,g=rx,o=rx
```

This represents permissions for **user, group, and others**.

---

### Setting `umask`

`umask` can be configured temporarily or permanently.

---

### Temporary Setting (Current Shell Session)

```
umask 027
```

This applies only to the current shell session and resets when the terminal is closed.

---

### Permanent Setting (User Level)

Add the `umask` value to shell configuration files such as:

```
~/.bashrc
~/.profile
```

Example:

```
echo "umask 027" >> ~/.bashrc
```

---

### System-Wide Default

To set `umask` for all users, configure it in:

```
/etc/profile
```

or

```
/etc/login.defs
```

---

### Practical Examples

Restrict files to owner only:

```
umask 077
touch secret.txt
ls -l secret.txt
```

Output:

```
-rw-------
```

Only the **owner can read and write the file**.

---

Allow group read but restrict others:

```
umask 027
mkdir project
ls -ld project
```

Output:

```
drwxr-x---
```

The owner has full access, the group can read/execute, and others have no access.

---

### Tricky Interview Questions

Why are directories executable but files are not by default?

Directories require the **execute (`x`) permission** to allow users to **enter the directory (`cd`) and list contents**.  
Files only require execute permission if they are **scripts or executable programs**.

---

How does `umask` affect a new file created with `touch`?

The file starts with default permissions (`666`), and the `umask` value removes specific permissions to determine the final permissions.

---

Difference between `umask 022` and `umask 002`?

| umask | Result |
|------|-------|
| `022` | Owner full access, group and others read-only |
| `002` | Owner full access, group full access, others read-only |

---

How can you temporarily allow group write access for all new files?

```
umask 002
```

This allows **both owner and group to write to new files**, which is useful in collaborative environments.

---

### Interview Summary

The `umask` command controls the **default permission mask applied to newly created files and directories**. It improves security by removing unnecessary permissions from system defaults and ensures proper access control based on user, group, and other permissions.

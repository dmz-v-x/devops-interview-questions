### Question
What are the different types of permissions in Linux and how do you change them?

### Answer

Linux uses a **permission model** to control access to files and directories. Each file or directory has permissions assigned to different types of users, determining who can read, write, or execute it.

The permission system is based on **three types of users** and **three types of permissions**.

---

### Types of Users

| User Type | Symbol | Description |
|----------|--------|-------------|
| Owner | `u` | The user who owns the file |
| Group | `g` | Users who belong to the file’s group |
| Others | `o` | All other users on the system |

---

### Types of Permissions

| Permission | Symbol | Description |
|-----------|--------|-------------|
| Read | `r` | Allows viewing the contents of a file or listing directory contents |
| Write | `w` | Allows modifying a file or creating/deleting files in a directory |
| Execute | `x` | Allows running a file as a program or accessing a directory |

Example permission string:

    -rwxr-xr--

Explanation:

- `rwx` → Owner can read, write, and execute  
- `r-x` → Group can read and execute  
- `r--` → Others can only read  

---

### Viewing File Permissions

Use the `ls -l` command:

    ls -l filename

Example output:

    -rw-r--r-- 1 user group 1234 Aug 19 10:00 file.txt

This shows the permission structure, owner, group, file size, and timestamp.

---

### Changing Permissions Using `chmod`

Permissions can be modified using the `chmod` command. There are two methods: **symbolic mode** and **numeric (octal) mode**.

---

### Symbolic Mode

Syntax:

    chmod [who][operator][permission] filename

Who:

- `u` → owner  
- `g` → group  
- `o` → others  
- `a` → all users (owner, group, others)

Operators:

- `+` → add permission  
- `-` → remove permission  
- `=` → set exact permission

Permissions:

- `r`, `w`, `x`

Examples:

    chmod u+x file.txt
    chmod g-w file.txt
    chmod o=r file.txt
    chmod a+r file.txt

Explanation:

- Add execute permission for owner
- Remove write permission from group
- Set others to read-only
- Give read permission to everyone

---

### Numeric (Octal) Mode

Permissions can also be represented numerically.

| Permission | Value |
|-----------|------|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

These values are combined to set permissions for **owner, group, and others**.

Example:

    chmod 755 file.txt

Explanation:

| User | Value | Permission |
|------|------|-----------|
| Owner | 7 (4+2+1) | rwx |
| Group | 5 (4+0+1) | r-x |
| Others | 5 (4+0+1) | r-x |

Another example:

    chmod 644 file.txt

Explanation:

| User | Value | Permission |
|------|------|-----------|
| Owner | 6 (4+2) | rw- |
| Group | 4 | r-- |
| Others | 4 | r-- |

---

### Changing Ownership

Ownership can be modified using `chown` and `chgrp`.

Change owner and group:

    sudo chown user:group file.txt

Change only the group:

    sudo chgrp group file.txt

---

### Special Permissions

Linux also supports special permission bits.

Setuid:

Runs executable with the **owner’s privileges**.

    chmod u+s program

Setgid:

Runs executable with **group privileges**, and directories allow new files to inherit the group.

    chmod g+s folder

Sticky Bit:

Only the file owner can delete files within the directory.

    chmod +t /tmp

---

### Checking Permissions Recursively

List permissions recursively:

    ls -lR /path/to/directory

Apply permissions recursively:

    chmod -R 755 /path/to/directory

---

### Practical Examples

Make a script executable only by the owner:

    chmod 700 script.sh

Make a web directory readable by everyone but writable only by the owner:

    chmod 755 /var/www/html

Ensure files in the temporary directory cannot be deleted by other users:

    chmod +t /tmp

---

### Tricky Interview Questions

Difference between:

    chmod 777

and

    chmod a+rwx

Both give read, write, and execute permissions to all users. The numeric format is compact, while symbolic mode is more descriptive.

---

What is the sticky bit?

The sticky bit ensures that **only the file owner can delete files inside a directory**, even if others have write permissions.

---

How to give execute permission to group and others but not owner?

    chmod u-x,g+x,o+x script.sh

---

How to set a default group for new files in a directory?

    chmod g+s /directory

---

### Interview Summary

Linux permissions control access to files and directories using three user categories (owner, group, others) and three permission types (read, write, execute). Permissions can be modified using `chmod` in symbolic or numeric mode, while ownership can be changed using `chown` and `chgrp`.

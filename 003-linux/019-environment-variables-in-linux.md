### Question
Explain the use of environment variables in Linux.

### Answer

Environment variables in Linux are **dynamic values stored by the operating system** that influence the behavior of the shell and running programs. They define the **environment in which processes execute**, including system paths, user information, language settings, and application configuration.

Programs and scripts read these variables to determine how they should behave.

---

### What Are Environment Variables?

Environment variables are:

- Dynamic values maintained by the shell or operating system
- Used to configure the environment for programs and scripts
- Passed to **child processes** so they inherit the environment of the parent shell

They commonly store:

- executable search paths
- user information
- system configuration
- language and locale settings

---

### Examples of Common Environment Variables

| Variable | Purpose |
|--------|---------|
| `PATH` | Directories where the system searches for executable files |
| `HOME` | Current user's home directory |
| `USER` | Username of the logged-in user |
| `SHELL` | Default shell used by the user |
| `PWD` | Current working directory |
| `LANG` | Language and locale settings |
| `EDITOR` | Default text editor used by programs |

---

### Viewing Environment Variables

You can view environment variables using several commands.

View all environment variables:

```
printenv
```

or

```
env
```

View a specific variable:

```
echo $HOME
echo $PATH
```

List all shell variables (including environment and local variables):

```
set
```

---

### Setting Environment Variables

Environment variables can be configured **temporarily or permanently**.

---

### Temporary Variables (Current Session Only)

Set a variable for the current shell session:

```
export MY_VAR="Hello"
```

Check the value:

```
echo $MY_VAR
```

Output:

```
Hello
```

This variable will disappear when the terminal session ends.

---

### Permanent Variables (All Sessions)

To make variables persistent across sessions, add them to configuration files such as:

- `~/.bashrc`
- `~/.bash_profile`
- `/etc/profile` (system-wide)

Example:

```
export MY_VAR="Hello"
```

After editing the file, reload it:

```
source ~/.bashrc
```

---

### Example: The `PATH` Variable

The `PATH` variable determines where the shell searches for executable programs.

Check current PATH:

```
echo $PATH
```

Example output:

```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Add a custom directory to PATH:

```
export PATH=$PATH:/home/user/scripts
```

This allows programs in `/home/user/scripts` to be executed without specifying the full path.

---

### Using Environment Variables in Scripts

Environment variables can be used inside shell scripts.

Example script:

```
#!/bin/bash
echo "Hello, $USER!"
echo "Your home directory is $HOME"
```

The output depends on the environment of the user running the script.

---

### Tricky Interview Questions

What is the difference between a shell variable and an environment variable?

| Type | Description |
|------|-------------|
| Shell Variable | Exists only in the current shell session |
| Environment Variable | Exported and accessible to child processes |

---

How do you make a variable accessible to child processes?

```
MY_VAR="Hello"
export MY_VAR
```

---

How do you temporarily modify `PATH` for a single command?

```
PATH=/my/custom/path:$PATH mycommand
```

This change applies only to that command execution.

---

How do you remove an environment variable?

```
unset MY_VAR
```

---

How do you view only exported variables?

```
export -p
```

---

### Interview Summary

Environment variables store configuration values that influence how processes and applications run in Linux. They define system paths, user settings, and runtime configurations, and can be viewed, modified, exported, or removed using shell commands.

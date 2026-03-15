### Question
What does the `nohup` command do, and why is it used?

### Answer

The `nohup` command in Linux is used to run a command **immune to the SIGHUP (hangup) signal**.  
`nohup` stands for **“no hang up.”**

Normally, when a terminal session is closed (for example, when a user logs out or an SSH session disconnects), the system sends a **SIGHUP signal** to processes started in that terminal. This signal typically causes those processes to terminate.

`nohup` prevents this behavior, allowing a process to **continue running even after the terminal session ends**.

---

### What is `nohup`?

`nohup` is a command used to execute another command such that it **ignores the SIGHUP signal**.

Key idea:

- It prevents processes from terminating when the terminal closes.
- It allows programs to continue running **after logout or terminal exit**.

---

### Why is `nohup` Used?

`nohup` is commonly used for **long-running processes**, especially when working on remote systems.

Typical scenarios include:

- Running **backup jobs**
- Starting **servers** (such as Python, Node.js, or application servers)
- Executing **long-running scripts**
- Running jobs during **remote SSH sessions**

Example situation:

If you start a script on a remote server via SSH and then disconnect, the process would normally terminate. Using `nohup` ensures it **keeps running even after you disconnect**.

---

### How `nohup` Works

When a command is run with `nohup`:

- The process **ignores the SIGHUP signal**
- Standard output (`stdout`) is redirected to **`nohup.out`** if not specified
- Standard error (`stderr`) is also redirected to **`nohup.out`**

This ensures that the process does not rely on a terminal for input/output.

---

### Basic Syntax

```
nohup command [arguments] &
```

Explanation:

- `nohup` → prevents termination on terminal hangup
- `command` → the program or script to run
- `&` → runs the process in the **background**

Without `&`, the command will still survive logout, but it will remain **attached to the terminal until the terminal is closed**.

---

### Examples

Run a script in the background:

```
nohup ./long_script.sh &
```

By default, output will be written to:

```
nohup.out
```

---

Redirect output explicitly:

```
nohup ./long_script.sh > output.log 2>&1 &
```

Explanation:

- `> output.log` → redirects standard output
- `2>&1` → redirects standard error to the same file

This is commonly used in production to store logs in a custom file.

---

Check if the process is running:

```
ps -ef | grep long_script.sh
```

This displays the running process in the process list.

---

### Difference Between `&` and `nohup`

Running a command with `&`:

```
command &
```

This starts the process in the background but **does not protect it from terminal logout**.

Running a command with `nohup` and `&`:

```
nohup command &
```

This runs the command in the background **and ensures it continues running after logout**.

---

### Related Commands

Other commands can achieve similar goals depending on the use case.

`disown`

Removes a job from the shell’s job table so it continues running after logout.

Example:

```
disown %1
```

---

`screen` or `tmux`

These are **terminal multiplexers** that allow interactive sessions to continue running.

They allow users to:

- detach from a session
- reconnect later
- continue interacting with running programs

Unlike `nohup`, they support **interactive processes**.

---

### Tricky Interview Questions

Why does `nohup` create a `nohup.out` file?

Because when the terminal closes, the process no longer has a connected terminal for **stdout or stderr**, so `nohup` redirects output to `nohup.out`.

---

What happens if you don’t use `nohup` and close the terminal?

The running process receives a **SIGHUP signal**, which usually causes it to terminate.

---

Can you use `nohup` without `&`?

Yes.  
The command will ignore SIGHUP and continue after logout, but it will **remain in the foreground until the terminal is closed or output is redirected**.

---

How is `nohup` different from `screen` or `tmux`?

| Tool | Purpose |
|---|---|
| `nohup` | Runs background non-interactive processes that survive logout |
| `screen` / `tmux` | Maintain interactive terminal sessions that can be detached and reattached |

---

### Interview Summary

The `nohup` command allows processes to continue running even after a user logs out or closes the terminal by ignoring the SIGHUP signal. It is commonly used for long-running jobs, server processes, and scripts executed on remote systems.

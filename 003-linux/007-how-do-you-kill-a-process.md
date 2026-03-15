### Question
How do you kill a process by name or Process ID (PID) in Linux?

### Answer

In Linux, processes can be terminated using commands such as `kill`, `killall`, and `pkill`. Each process has a unique **Process ID (PID)**, and you can terminate processes either by **PID** or by **process name**.

---

### Killing a Process by PID

Every running process in Linux is assigned a unique **Process ID (PID)**. You can terminate a process using the `kill` command.

Basic syntax:

    kill <PID>

Example:

    kill 1234

By default, this command sends the **SIGTERM (signal 15)** signal, which politely asks the process to terminate.

---

### Common Signals Used with `kill`

| Signal | Number | Description |
|------|------|-------------|
| SIGTERM | 15 | Graceful termination (default signal) |
| SIGKILL | 9 | Forcefully kills the process |
| SIGHUP | 1 | Reload configuration |
| SIGSTOP | 19 | Pause/suspend a process |

Force kill example:

    kill -9 1234

`SIGKILL` immediately stops the process and cannot be ignored by the application.

---

### Killing a Process by Name Using `killall`

The `killall` command allows you to terminate processes using the **process name** instead of PID.

Syntax:

    killall <process_name>

Example:

    killall apache2

This will terminate all processes with the name `apache2`.

Force kill example:

    killall -9 apache2

---

### Killing a Process Using `pkill`

`pkill` works similarly to `killall`, but it supports **pattern matching**.

Syntax:

    pkill <process_name>

Example:

    pkill ssh

Force kill example:

    pkill -9 ssh

Useful options:

| Option | Description |
|------|-------------|
| `-u username` | Kill processes belonging to a specific user |
| `-f` | Match the full command line |

Example:

    pkill -u user1 nginx

---

### Killing Processes Using `top` or `htop`

Both `top` and `htop` allow you to terminate processes interactively.

Using `top`:

    top

Press:

- `k` → enter the PID  
- press **Enter**  
- optionally specify the signal (default is 15)

Using `htop`:

    htop

Steps:

- Navigate to the process using arrow keys
- Press **F9**
- Select the signal to send
- Press **Enter**

---

### Steps to Safely Kill a Process

Step 1: Find the process

    ps aux | grep process_name

or

    pgrep process_name

---

Step 2: Attempt graceful termination

    kill <PID>

---

Step 3: Force kill if necessary

    kill -9 <PID>

---

### Best Practices

- Always try **SIGTERM (`kill`) first** before using **SIGKILL (`kill -9`)**.
- Confirm that the process has stopped:

    ps -p <PID>

- Use `pgrep` in scripts for automation:

    pgrep -u username process_name | xargs kill

- Be cautious when using `killall`, as it can terminate multiple processes.

---

### Summary Table

| Command | Kill by | Example | Notes |
|------|------|------|------|
| `kill` | PID | `kill 1234` | Default SIGTERM, use `-9` for force kill |
| `killall` | Process name | `killall apache2` | Terminates all processes with that name |
| `pkill` | Name or pattern | `pkill ssh` | Supports pattern matching |
| `top` | Interactive | `top → k → PID` | Allows sending signals interactively |
| `htop` | Interactive | `htop → F9 → signal` | Easier visual process management |

---

### Interview Summary

To terminate processes in Linux, you can use `kill` with a PID, `killall` or `pkill` with a process name, or interactive tools like `top` and `htop`. It is recommended to first use `SIGTERM` (`kill`) for graceful termination and only use `SIGKILL` (`kill -9`) if the process does not stop.

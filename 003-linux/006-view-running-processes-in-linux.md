### Question
How do you view running processes in Linux?

### Answer

Linux provides several commands to view and monitor running processes. These tools help administrators inspect active programs, analyze CPU or memory usage, and troubleshoot system performance issues.

The most commonly used commands include `ps`, `top`, `htop`, `pgrep`, `pidof`, and the `/proc` filesystem.

---

### Using the `ps` Command (Process Status)

The `ps` command shows a snapshot of the current processes running on the system.

Basic usage:

    ps

This shows processes running in the current shell.

Commonly used options:

| Command | Description |
|--------|-------------|
| `ps -e` or `ps -A` | Show all running processes |
| `ps -f` | Full format output including user, PID, PPID, start time |
| `ps -ef` | Detailed listing of all processes |
| `ps -u username` | Show processes for a specific user |
| `ps aux` | BSD-style output with detailed process information |

Example:

    ps aux | grep apache

This displays all running processes that contain the word **apache**.

---

### Using the `top` Command

`top` provides a **real-time interactive view** of system processes.

Usage:

    top

Features:

- Displays CPU usage, memory usage, and process information
- Continuously updates process statistics
- Shows system load averages

Useful interactive keys inside `top`:

| Key | Function |
|----|----------|
| `P` | Sort processes by CPU usage |
| `M` | Sort processes by memory usage |
| `k` | Kill a process using its PID |
| `q` | Quit the program |

---

### Using the `htop` Command

`htop` is an improved version of `top` with a more user-friendly interface.

Usage:

    htop

Features:

- Color-coded display of CPU, memory, and swap usage
- Scrollable process list
- Easy process management
- Interactive navigation using arrow keys

Installation examples:

Debian/Ubuntu:

    sudo apt install htop

RHEL/CentOS:

    sudo yum install htop

---

### Using the `pgrep` Command

`pgrep` searches for processes by name and returns their process IDs (PIDs).

Example:

    pgrep apache

This returns the PIDs of all running Apache processes.

To display detailed information:

    ps -fp $(pgrep apache)

---

### Using the `pidof` Command

`pidof` returns the process ID of a running program.

Example:

    pidof sshd

This shows the PID of the `sshd` process.

---

### Using the `/proc` Filesystem

Linux maintains a virtual filesystem called `/proc` that contains detailed information about running processes.

Each running process has a directory named after its PID.

Example:

List all process directories:

    ls /proc

View detailed information for a specific process:

    cat /proc/1/status

This displays details for the process with PID `1`.

---

### Summary of Commands

| Command | Purpose |
|-------|---------|
| `ps` | Displays a snapshot of running processes |
| `top` | Real-time process monitoring |
| `htop` | Interactive process viewer with enhanced UI |
| `pgrep` | Search processes by name |
| `pidof` | Retrieve PID of a running program |
| `/proc` filesystem | Access detailed process information |

---

### Interview Summary

Running processes in Linux can be viewed using commands such as `ps` for process snapshots, `top` or `htop` for real-time monitoring, `pgrep` or `pidof` to find processes by name, and the `/proc` filesystem for detailed process information.

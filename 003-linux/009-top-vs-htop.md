### Question
Explain the use of `top` and `htop` for monitoring processes in Linux.

### Answer

`top` and `htop` are interactive Linux commands used for **real-time system monitoring**. They allow administrators to observe running processes, CPU usage, memory consumption, and system performance.

These tools are especially useful for **identifying resource-intensive processes, troubleshooting performance issues, and managing running processes**.

---

### Using the `top` Command

`top` is a built-in Linux command that provides a **dynamic, real-time view of system processes and resource usage**.

Basic usage:

    top

Key information displayed:

- CPU usage
- Memory usage
- Swap usage
- Process ID (PID)
- User running the process
- Priority and nice value
- CPU percentage (`%CPU`)
- Memory usage (`%MEM`)
- Command name

The display updates periodically (default: **every 3 seconds**).

---

### Interactive Commands in `top`

While `top` is running, you can use keyboard shortcuts to interact with processes.

| Key | Action |
|----|-------|
| `P` | Sort processes by CPU usage |
| `M` | Sort processes by memory usage |
| `N` | Sort processes by PID |
| `T` | Sort by running time |
| `k` | Kill a process (enter PID and signal) |
| `r` | Renice a process (change priority) |
| `q` | Quit `top` |

Examples:

Monitor processes of a specific user:

    top -u username

Monitor a specific process ID:

    top -p 1234

---

### Using the `htop` Command

`htop` is an **enhanced and more user-friendly version of `top`**. It provides better visualization and easier process management.

Usage:

    htop

Installation examples:

Debian/Ubuntu:

    sudo apt install htop

RHEL/CentOS:

    sudo yum install htop

Key features:

- Color-coded display for CPU, memory, and swap
- Scrollable process list
- Interactive process management
- Process tree view
- Easy sorting and filtering

---

### Interactive Controls in `htop`

| Key | Action |
|----|-------|
| `F3` | Search for a process |
| `F4` | Filter processes by name |
| `F6` | Sort by selected column |
| `F9` | Kill a process |
| `F7` | Increase process priority |
| `F8` | Decrease process priority |

You can navigate using **arrow keys** and manage processes directly.

---

### Differences Between `top` and `htop`

| Feature | `top` | `htop` |
|-------|-------|--------|
| Display | Plain text interface | Color-coded interactive UI |
| Navigation | Limited | Scrollable with keyboard |
| Process management | Basic shortcuts | Interactive F-key controls |
| Process tree view | Not available | Available |
| Customization | Limited | Highly customizable |

---

### Practical Use Cases

Identify CPU-heavy processes:

    top

Then press:

    P

to sort by CPU usage.

Monitor memory consumption:

    htop

Then sort by memory usage.

Manage processes interactively:

    htop

Select a process and press:

- `F9` to kill the process
- `F7` to increase priority
- `F8` to decrease priority

---

### Interview Summary

`top` and `htop` are real-time Linux process monitoring tools. `top` is a built-in command that displays system resource usage and running processes, while `htop` is an enhanced version with a more interactive interface, color-coded output, and easier process management.

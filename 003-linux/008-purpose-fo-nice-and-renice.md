### Question
What is the purpose of the `nice` and `renice` commands in Linux?

### Answer

In Linux, the CPU scheduler decides how much CPU time each process receives.  
The **nice value** controls the **priority of a process** in relation to others.

The commands `nice` and `renice` are used to adjust this priority:

- `nice` → sets the priority **when starting a new process**
- `renice` → changes the priority of an **already running process**

Their purpose is to manage CPU resource usage so that heavy background tasks do not interfere with critical processes.

---

### The Nice Value

Each process has a **nice value** that determines its scheduling priority.

Range:

- **-20** → Highest priority (gets more CPU time)
- **0** → Default priority
- **19** → Lowest priority (gets less CPU time)

Important rules:

- Only the **root user** can assign negative values (increase priority).
- Regular users can only **increase the nice value** (reduce priority).

---

### Using the `nice` Command

The `nice` command starts a program with a specified priority.

Syntax:

    nice -n <nice_value> command

Examples:

Run a program with default nice value:

    nice ./backup.sh

Run a program with lower priority:

    nice -n 10 ./backup.sh

Run a program with higher priority (requires root):

    sudo nice -n -5 ./important_task.sh

Check the nice value of a running process:

    ps -o pid,comm,nice -p <PID>

---

### Using the `renice` Command

`renice` is used to modify the priority of an **existing running process**.

Syntax:

    renice <new_nice_value> -p <PID>

Examples:

Lower priority of a running process:

    renice 15 -p 1234

Change priority of multiple processes:

    renice 10 -p 1234 5678

Change priority of all processes belonging to a user:

    renice 5 -u username

---

### Checking Process Priority

You can view the nice value of processes using tools like `top`, `htop`, or `ps`.

Using `top`:

    top

Look at the **NI column**, which shows the nice value.

Using `ps`:

    ps -o pid,user,ni,comm -p <PID>

---

### Comparison: `nice` vs `renice`

| Feature | `nice` | `renice` |
|-------|-------|----------|
| When used | When starting a new process | For an already running process |
| Purpose | Set initial process priority | Modify priority of running process |
| Command example | `nice -n 10 command` | `renice 15 -p 1234` |
| Root privileges | Required for negative nice values | Required to decrease nice value |

---

### Practical Example

Scenario: A heavy backup script should run without affecting the performance of a web server.

Solution:

    nice -n 15 ./backup.sh

This runs the backup script with a **lower priority**, allowing the web server to receive CPU resources first.

---

### Interview Summary

The `nice` command sets the CPU scheduling priority when starting a new process, while `renice` changes the priority of an already running process. Nice values range from **-20 (highest priority)** to **19 (lowest priority)** and help control how CPU resources are distributed among processes.

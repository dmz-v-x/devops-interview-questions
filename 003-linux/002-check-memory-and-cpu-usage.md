### Question
How do you check the CPU and memory usage of a Linux system? Mention different commands used for monitoring.

### Answer

In Linux, there are several commands used to monitor **CPU usage, memory usage, and overall system performance**. These tools help administrators identify resource bottlenecks, troubleshoot performance issues, and monitor system health.

These commands can be grouped into two categories:

- CPU monitoring commands
- Memory monitoring commands

---

### Checking CPU Usage

Linux provides multiple tools to monitor CPU activity and process utilization.

#### `top`

`top` is one of the most commonly used interactive commands for monitoring system resources in real time.

    top

Key columns:

- `%CPU` → CPU usage per process  
- `%MEM` → Memory usage per process  
- `load average` → system load over the last 1, 5, and 15 minutes  

Useful shortcuts inside `top`:

- `P` → sort by CPU usage  
- `M` → sort by memory usage  
- `q` → quit the program  

---

#### `htop` (Enhanced version of top)

`htop` is an improved, interactive version of `top` with a more user-friendly interface.

    htop

Features:

- Colorful display
- Scrollable process list
- Easy process management
- Ability to kill processes interactively

---

#### `mpstat` (CPU usage per core)

`mpstat` is part of the **sysstat package** and displays CPU usage statistics for each processor core.

    mpstat -P ALL 2 5

Explanation:

- `-P ALL` → show statistics for all CPU cores  
- `2` → collect data every 2 seconds  
- `5` → repeat the report 5 times  

---

#### `sar` (System Activity Report)

`sar` collects and reports system performance metrics such as CPU usage.

    sar -u 2 5

Explanation:

- `-u` → CPU utilization statistics  
- `2` → interval in seconds  
- `5` → number of reports  

---

#### `vmstat`

`vmstat` reports information about CPU, memory, and I/O.

    vmstat 2 5

Important CPU columns:

- `us` → user CPU usage  
- `sy` → system CPU usage  
- `id` → idle CPU percentage  

---

#### `uptime`

`uptime` displays how long the system has been running along with load averages.

    uptime

Example output:

    load average: 0.45, 0.50, 0.55

These values represent the average system load over:

- 1 minute
- 5 minutes
- 15 minutes

---

#### `ps` (Check CPU usage per process)

To find processes consuming the most CPU:

    ps aux --sort=-%cpu | head -10

This shows the top 10 CPU-consuming processes.

---

### Checking Memory Usage

Several commands help monitor RAM usage and memory consumption.

---

#### `free`

`free` displays total, used, and available memory.

    free -h

Explanation:

- `-h` → human-readable format (MB/GB)

Important columns:

- `total` → total RAM
- `used` → memory currently used
- `free` → unused memory
- `available` → memory available for applications

---

#### `vmstat` (Memory statistics)

`vmstat` also provides memory usage information.

    vmstat 2 5

Important memory columns:

- `swpd` → swap memory used  
- `free` → free memory  
- `buff` → buffer memory  
- `cache` → cached memory  

---

#### `top` / `htop`

Both commands display memory usage in real time.

You can also see memory usage per process using the `%MEM` column.

---

#### `/proc/meminfo`

Detailed memory information can be obtained from the system file:

    cat /proc/meminfo

Important fields include:

- `MemTotal`
- `MemFree`
- `Buffers`
- `Cached`
- `SwapTotal`
- `SwapFree`

---

#### `smem` (if installed)

`smem` provides more accurate memory usage by considering shared memory.

    smem -r

This tool is useful when analyzing memory usage across processes.

---

#### `ps` (Check memory usage per process)

To identify processes consuming the most memory:

    ps aux --sort=-%mem | head -10

This displays the top 10 memory-consuming processes.

---

### Disk and Swap Checks

You can also check related system resources.

Check swap memory usage:

    swapon -s

or

    free -h

Check disk space usage:

    df -h

Check disk usage by directories:

    du -sh /path

---

### Combined CPU and Memory Monitoring Tools

| Tool | Type | Description |
|-----|------|-------------|
| `top` | Interactive | Real-time CPU and memory monitoring |
| `htop` | Interactive | Improved visual process monitor |
| `vmstat` | CLI | CPU, memory, and I/O statistics |
| `sar` | CLI | Historical system performance data |
| `glances` | Interactive | Comprehensive system monitoring |

---

### Example: Quick System Health Check

Check system load:

    uptime

Check memory usage:

    free -h

Check top CPU-consuming processes:

    ps aux --sort=-%cpu | head -10

Check top memory-consuming processes:

    ps aux --sort=-%mem | head -10

Monitor system resources in real time:

    top

---

### Key Notes

- `%CPU` shows how much CPU a process is using.  
- `100% CPU` typically means a process fully occupies one CPU core.  
- Memory usage includes buffers and cache, so low "free memory" does not necessarily mean the system is out of memory.  
- Tools like `htop` and `glances` are easier for real-time monitoring and troubleshooting.

---

### Interview Summary

Linux provides several commands to monitor CPU and memory usage such as `top`, `htop`, `mpstat`, `sar`, `vmstat`, `uptime`, `free`, and `ps`. These tools help administrators analyze system performance, identify resource-intensive processes, and troubleshoot performance issues.

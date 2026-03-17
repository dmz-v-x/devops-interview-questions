### Question  
How does this Shell Script monitor system processes and memory usage, and how does it work step by step?

---

### Answer  

### Complete Script  

    #!/bin/bash
    # System Processes & Memory Monitoring Script

    MEMORY_THRESHOLD=90
    CPU_THRESHOLD=80

    # Memory Usage Check
    memory_usage=$(free | awk '/Mem/{printf "%.0f", $3/$2*100}')
    echo "Memory Usage: $memory_usage%"

    if [ "$memory_usage" -gt "$MEMORY_THRESHOLD" ]; then
        echo "ALERT: High memory usage!" >&2
    fi

    # CPU Usage Check
    cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')
    echo "CPU Usage: ${cpu_usage}%"

    if (( $(echo "$cpu_usage > $CPU_THRESHOLD" | bc -l) )); then
        echo "ALERT: High CPU usage!" >&2
        exit 1
    fi

    # Top 5 Processes
    echo -e "\nTop 5 Processes:"
    ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -6

---

### 1. Script Overview  

This script monitors system health by:

- Checking **memory usage**  
- Checking **CPU usage**  
- Alerting if thresholds are exceeded  
- Displaying top memory-consuming processes  

---

### 2. Code Breakdown  

---

#### Shebang  

    #!/bin/bash

- Runs the script using **Bash shell**

---

#### Threshold Configuration  

    MEMORY_THRESHOLD=90
    CPU_THRESHOLD=80

- Defines alert limits:
  - Memory → 90%  
  - CPU → 80%  

---

#### Memory Usage Calculation  

    memory_usage=$(free | awk '/Mem/{printf "%.0f", $3/$2*100}')

Breakdown:

1. `free`:
   - Shows memory usage  

2. `awk '/Mem/'`:
   - Extracts memory row  

3. `$3/$2*100`:
   - Used / Total * 100  

4. `printf "%.0f"`:
   - Rounds to integer  

---

#### Print Memory Usage  

    echo "Memory Usage: $memory_usage%"

---

#### Memory Alert  

    if [ "$memory_usage" -gt "$MEMORY_THRESHOLD" ]; then
        echo "ALERT: High memory usage!" >&2
    fi

- Compares usage with threshold  
- Sends alert to **stderr**  

---

#### CPU Usage Calculation  

    cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')

Breakdown:

1. `top -bn1`:
   - Runs `top` in batch mode (non-interactive)  

2. `grep "Cpu(s)"`:
   - Extracts CPU stats line  

3. `$8`:
   - Represents **idle CPU %**  

4. `100 - idle`:
   - Gives **actual CPU usage**  

---

#### Print CPU Usage  

    echo "CPU Usage: ${cpu_usage}%"

---

#### CPU Alert  

    if (( $(echo "$cpu_usage > $CPU_THRESHOLD" | bc -l) )); then
        echo "ALERT: High CPU usage!" >&2
        exit 1
    fi

- Uses `bc` for floating-point comparison  
- Exits script if threshold exceeded  

---

#### Display Top Processes  

    echo -e "\nTop 5 Processes:"
    ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -6

Breakdown:

1. `ps -eo`:
   - Displays process info  

2. Columns:
   - `pid` → Process ID  
   - `ppid` → Parent ID  
   - `cmd` → Command  
   - `%mem` → Memory usage  
   - `%cpu` → CPU usage  

3. `--sort=-%mem`:
   - Sorts by memory usage (descending)  

4. `head -6`:
   - Top 5 processes + header  

---

### 3. Execution Flow  

1. Script starts  
2. Sets thresholds  
3. Calculates memory usage  
4. Prints memory usage  
5. Checks memory threshold  
6. Calculates CPU usage  
7. Prints CPU usage  
8. Checks CPU threshold  
9. If exceeded → alert and exit  
10. Displays top 5 processes  

---

### 4. Real-World Use Cases  

---

Monitor server health:

    ./monitor.sh

---

Used in cron jobs:

    */5 * * * * /path/to/monitor.sh

---

Detect resource bottlenecks in production  

---

Debug high memory/CPU usage  

---

---

### 5. Improvements / Best Practices  

---

#### Add Logging  

    echo "$(date) CPU=$cpu_usage MEM=$memory_usage" >> monitor.log

---

#### Send Alerts (Email/Slack)  

    echo "High CPU usage" | mail -s "Alert" admin@example.com

---

#### Monitor Disk Usage  

    df -h

---

#### Show Top CPU Processes  

    ps -eo pid,cmd,%cpu --sort=-%cpu | head -6

---

#### Use `htop` for interactive view  

---

### 6. Tricky Interview Questions  

---

Why use `top -bn1`?  

- Batch mode → script-friendly output  

---

What does `$8` represent in `top` output?  

- Idle CPU percentage  

---

Why subtract from 100?  

- CPU usage = 100 - idle  

---

Why use `bc`?  

- Bash cannot handle floating-point comparisons  

---

Difference between `%mem` and `%cpu`?  

| Metric | Meaning |
|---|---|
| %mem | Memory usage |
| %cpu | CPU usage |

---

### Interview Summary  

This script monitors system health by calculating memory and CPU usage, comparing them against thresholds, and displaying top resource-consuming processes. It is commonly used in monitoring, alerting systems, and DevOps automation.

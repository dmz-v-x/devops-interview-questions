### Question  
How does this Shell Script check system uptime, and how does it work step by step?

---

### Answer  

### Complete Script  

    #!/bin/bash
    # System Uptime Check Script

    UPTIME=$(uptime -p | cut -d' ' -f2-)
    UPTIME_SECONDS=$(awk '{print int($1)}' /proc/uptime)
    DAYS_UP=$((UPTIME_SECONDS / 86400))

    echo "System has been up: $UPTIME"

    # Alert if uptime > 90 days
    if [ "$DAYS_UP" -gt 90 ]; then
        echo "WARNING: System uptime exceeds 90 days!" >&2
        exit 1
    fi

---

### 1. Script Overview  

This script checks how long the system has been running and:

- Displays human-readable uptime  
- Calculates uptime in days  
- Triggers a warning if uptime exceeds **90 days**  

---

### 2. Code Breakdown  

---

#### Shebang  

    #!/bin/bash

- Executes the script using the **Bash shell**

---

#### Get Human-Readable Uptime  

    UPTIME=$(uptime -p | cut -d' ' -f2-)

Breakdown:

1. `uptime -p`:
   - Outputs uptime in readable format  
   - Example:

        up 2 days, 3 hours, 10 minutes  

2. `cut -d' ' -f2-`:
   - Removes the word `up`  
   - Keeps the rest of the string  

Result stored in:

    2 days, 3 hours, 10 minutes  

---

#### Get Uptime in Seconds  

    UPTIME_SECONDS=$(awk '{print int($1)}' /proc/uptime)

- `/proc/uptime` contains system uptime in seconds  

Example content:

    123456.78 234567.89  

- `awk '{print int($1)}'`:
  - Extracts first value  
  - Converts it to integer  

---

#### Convert Seconds to Days  

    DAYS_UP=$((UPTIME_SECONDS / 86400))

- 1 day = **86400 seconds**  
- Converts uptime into days  

---

#### Display Uptime  

    echo "System has been up: $UPTIME"

- Prints human-readable uptime  

---

#### Condition Check  

    if [ "$DAYS_UP" -gt 90 ]; then

- Checks if uptime exceeds **90 days**

---

#### Warning Case  

    echo "WARNING: System uptime exceeds 90 days!" >&2
    exit 1

- Prints warning to **stderr**  
- Exits script with failure status  

---

### 3. Execution Flow  

1. Script starts  
2. Fetches readable uptime  
3. Reads uptime in seconds  
4. Converts seconds → days  
5. Prints uptime  
6. Checks if uptime > 90 days  
7. If yes → prints warning and exits  
8. Otherwise → exits normally  

---

### 4. Real-World Use Cases  

---

Detect systems needing reboot:

    ./uptime_check.sh

---

Used in monitoring tools (Nagios, scripts, cron)  

---

Prevent long-running systems causing issues (memory leaks, kernel updates pending)  

---

---

### 5. Improvements / Best Practices  

---

#### Make Threshold Configurable  

    MAX_DAYS=90

    if [ "$DAYS_UP" -gt "$MAX_DAYS" ]; then

---

#### Add Logging  

    echo "$(date) - Uptime: $UPTIME" >> uptime.log

---

#### Send Alert (Email/Slack)  

    echo "System uptime too high" | mail -s "Uptime Alert" admin@example.com

---

#### Use `bc` for More Precision  

    DAYS_UP=$(echo "$UPTIME_SECONDS/86400" | bc)

---

### 6. Tricky Interview Questions  

---

What is `/proc/uptime`?  

- A virtual file containing:
  - Total uptime  
  - Idle time  

---

Why use `awk` here?  

- To extract and format numeric data  

---

Why divide by 86400?  

- Converts seconds → days  

---

Difference between `uptime` and `/proc/uptime`?  

| Command/File | Output |
|---|---|
| `uptime` | Human-readable |
| `/proc/uptime` | Raw numeric data |

---

Why send output to `stderr`?  

- For proper error handling in scripts and monitoring systems  

---

### Interview Summary  

This script checks system uptime using both human-readable and raw system data. It converts uptime into days and raises alerts when a threshold is exceeded, making it useful for system monitoring and maintenance automation.

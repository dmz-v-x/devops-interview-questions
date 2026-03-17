### Question  
How does this Shell Script check network connectivity, and how does it work step by step?

---

### Answer  

### Complete Script  

    #!/bin/bash
    # Network Connectivity Check Script

    # Targets to check (space-separated)
    TARGETS="8.8.8.8 google.com github.com"

    for target in $TARGETS; do
        if ping -c 3 -W 2 "$target" &> /dev/null; then
            echo "[SUCCESS] $target is reachable"
        else
            echo "[FAILURE] $target is unreachable" >&2
            exit 1
        fi
    done

---

### 1. Script Overview  

This **Bash script** checks whether multiple hosts (IPs or domains) are reachable over the network.

It:

- Loops through a list of targets  
- Uses `ping` to test connectivity  
- Prints success or failure  
- Stops execution if any target is unreachable  

---

### 2. Code Breakdown  

---

#### Shebang  

    #!/bin/bash

- Tells the system to run the script using the **Bash shell**

---

#### Define Targets  

    TARGETS="8.8.8.8 google.com github.com"

- A space-separated list of hosts to check  
- Can include:
  - IP addresses  
  - Domain names  

---

#### Loop Through Targets  

    for target in $TARGETS; do

- Iterates over each target one by one  
- Splits the string based on spaces  

---

#### Ping Check  

    if ping -c 3 -W 2 "$target" &> /dev/null; then

- Sends ICMP requests to check connectivity  

Options:

| Option | Meaning |
|---|---|
| `-c 3` | Send 3 packets |
| `-W 2` | Wait max 2 seconds per reply |

- `&> /dev/null`:
  - Redirects both output and errors  
  - Makes the script silent  

---

#### Success Case  

    echo "[SUCCESS] $target is reachable"

- Executes if `ping` succeeds  

---

#### Failure Case  

    echo "[FAILURE] $target is unreachable" >&2
    exit 1

- Prints error message to **stderr**  
- Exits script immediately with failure status  

---

#### End Loop  

    done

- Ends the loop  

---

### 3. Execution Flow  

1. Script starts  
2. Loads target list  
3. For each target:
   - Sends 3 ping requests  
   - Waits for response  
4. If reachable → prints success  
5. If not reachable → prints error and exits  
6. Stops at first failure  

---

### 4. Real-World Use Cases  

---

Check internet connectivity:

    ping -c 3 8.8.8.8

---

Verify DNS resolution:

    ping google.com

---

Used in DevOps monitoring scripts:

    TARGETS="db.internal api.service.com cache.local"

---

CI/CD health checks before deployment  

---

### 5. Improvements / Best Practices  

---

#### Continue Instead of Exit  

    FAILED=0

    for target in $TARGETS; do
        if ping -c 3 -W 2 "$target" &> /dev/null; then
            echo "[SUCCESS] $target is reachable"
        else
            echo "[FAILURE] $target is unreachable" >&2
            FAILED=1
        fi
    done

    exit $FAILED

---

#### Add Timeout Protection  

    timeout 5 ping -c 3 "$target"

---

#### Add Logging  

    echo "$(date) - Checking $target" >> network.log

---

### 6. Tricky Interview Questions  

---

Why use `&> /dev/null`?  

- To suppress output and rely only on exit status  

---

What does `ping` return on failure?  

- A non-zero exit code  

---

Why use `exit 1`?  

- Indicates failure (useful in scripts and pipelines)  

---

Difference between stdout and stderr?  

| Stream | Purpose |
|---|---|
| stdout (1) | Normal output |
| stderr (2) | Error messages |

---

### Interview Summary  

This script uses `ping` to check connectivity for multiple targets. It relies on exit codes to determine success or failure and is commonly used in automation, monitoring, and DevOps pipelines.

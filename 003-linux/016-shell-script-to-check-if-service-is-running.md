### Question
Write a shell script to check if a given service is running (for example `nginx`).

### Answer

In Linux, services can be checked using tools such as **systemctl**, **ps**, or the **service command** depending on the init system being used. A shell script can automate this check and report whether the service is running.

---

### Method 1: Using `systemctl` (Modern Linux Systems)

Most modern Linux distributions use **systemd** to manage services. The `systemctl is-active` command can be used to determine whether a service is running.

Example script:

```bash
#!/bin/bash

# Service name to check
SERVICE="nginx"

# Check if the service is active
if systemctl is-active --quiet $SERVICE
then
    echo "$SERVICE is running."
else
    echo "$SERVICE is NOT running."
fi
```

Explanation:

- `systemctl is-active --quiet SERVICE` checks the status of the service.
- It returns **exit code 0 if the service is running** and **non-zero if it is not**.
- The script uses a shell conditional:

```bash
if ... then ... else ... fi
```

to print the appropriate message.

---

### Running the Script

Make the script executable:

```bash
chmod +x check_service.sh
```

Run the script:

```bash
./check_service.sh
```

---

### Method 2: Using `ps` (Works on Any Linux System)

This method checks whether the process exists in the running process list. It works even on systems without **systemd**.

Example script:

```bash
#!/bin/bash

SERVICE="nginx"

# Check if process exists
if ps aux | grep -v grep | grep -q $SERVICE
then
    echo "$SERVICE is running."
else
    echo "$SERVICE is NOT running."
fi
```

Explanation:

- `ps aux` lists all running processes.
- `grep -v grep` excludes the grep process itself.
- `grep -q SERVICE` searches quietly and returns **exit code 0 if found**.

---

### Method 3: Using `service` Command (Older Init Systems)

Some older Linux systems use **SysVinit** or similar init systems instead of systemd.

Example script:

```bash
#!/bin/bash

SERVICE="nginx"

if service $SERVICE status > /dev/null 2>&1
then
    echo "$SERVICE is running."
else
    echo "$SERVICE is NOT running."
fi
```

Explanation:

- `service SERVICE status` checks the service status.
- `> /dev/null 2>&1` suppresses output and errors.
- The exit status determines whether the service is running.

---

### Bonus: Check and Restart Service if Not Running

This script checks whether the service is running and **attempts to start it if it is not**.

```bash
#!/bin/bash

SERVICE="nginx"

if systemctl is-active --quiet $SERVICE
then
    echo "$SERVICE is running."
else
    echo "$SERVICE is NOT running. Attempting to start..."
    sudo systemctl start $SERVICE
    if systemctl is-active --quiet $SERVICE
    then
        echo "$SERVICE started successfully."
    else
        echo "Failed to start $SERVICE."
    fi
fi
```

This is commonly used in **monitoring scripts or cron jobs** to ensure services remain active.

---

### Tricky Interview Questions

How can you check a service without using `systemctl`?

Use commands like:

```bash
ps aux | grep <service>
```

or

```bash
service <service-name> status
```

---

### Making the Script Accept a Service Name as an Argument

Instead of hardcoding the service name, you can pass it as a command-line argument.

Example script:

```bash
#!/bin/bash

SERVICE=$1

if [ -z "$SERVICE" ]; then
    echo "Usage: $0 <service-name>"
    exit 1
fi

if systemctl is-active --quiet $SERVICE
then
    echo "$SERVICE is running."
else
    echo "$SERVICE is NOT running."
fi
```

Run the script:

```bash
./check_service.sh nginx
```

---

### Checking Multiple Services at Once

You can loop through multiple services using an array.

Example:

```bash
#!/bin/bash

SERVICES=("nginx" "mysql" "ssh")

for S in "${SERVICES[@]}"; do
    systemctl is-active --quiet $S && echo "$S is running" || echo "$S is NOT running"
done
```

This script checks each service in the list and reports its status.

---

### Interview Summary

A shell script can check whether a service is running using commands like `systemctl`, `ps`, or `service`. The most common modern approach uses `systemctl is-active`, which returns an exit status indicating whether the service is running. Scripts can also be extended to restart services automatically or check multiple services at once.

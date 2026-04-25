### Question  
You are asked to monitor multiple services like nginx, sshd, and docker.  

Task:  
- Check the status of each service  
- If a service is stopped, attempt to restart it  
- Print a clearly formatted report  

---

### Answer  

---

### 1. Shell Script

```bash
#!/bin/bash

# List of services to monitor
services=("nginx" "sshd" "docker")

# Report Header
echo "-----------------------------------"
echo "  Service Health Check Report"
echo "-----------------------------------"

# Loop through services
for service in "${services[@]}"; do

  if systemctl is-active --quiet "$service"; then
    echo "$service is RUNNING"
  else
    echo "$service is STOPPED"
    echo ""
    echo "Attempting to restart $service..."

    systemctl restart "$service" &> /dev/null

    # Check if restart was successful
    if systemctl is-active --quiet "$service"; then
      echo "$service has been restarted successfully."
    else
      echo "Failed to restart $service. Manual intervention needed."
    fi
  fi

  echo "-----------------------------------"

done
```

---

### 2. How to Execute

```bash
chmod +x multi_service_monitor.sh
sudo ./multi_service_monitor.sh
```

- Requires root privileges for service management  

---

### 3. Example Output

```
-----------------------------------
  Service Health Check Report
-----------------------------------
nginx is RUNNING
-----------------------------------
sshd is RUNNING
-----------------------------------
docker is STOPPED

Attempting to restart docker...
docker has been restarted successfully.
-----------------------------------
```

---

### 4. Script Breakdown

- `services=("nginx" "sshd" "docker")`  
  - Array of services to monitor  

- `systemctl is-active --quiet <service>`  
  - Checks if service is running  

- `systemctl restart <service>`  
  - Attempts to restart stopped service  

- Loop:
  - Iterates through each service  
  - Performs health check + auto-recovery  

- Output formatting:
  - Clear separators for readability  

---

### 5. Enhancements (Best Practices)

- Add logging:

```bash
LOG_FILE="/var/log/service_monitor.log"
echo "$(date) - Checked $service" >> "$LOG_FILE"
```

- Add alerts (email/Slack) for failures  

- Add timeout handling for restart attempts  

- Run via cron:

```bash
*/5 * * * * /path/to/multi_service_monitor.sh
```

---

### 6. Key Takeaways

- Automates service health checks  
- Enables self-healing systems  
- Improves reliability and uptime  

---

### 7. Interview-Ready Summary

“I would write a shell script that iterates over a list of services, checks their status using systemctl, and attempts to restart any stopped services. After restarting, I would verify the status again and print a structured report. This ensures automated monitoring and quick recovery of critical services.”

### Question
How do you troubleshoot disk space issues on a CI/CD server?

### Answer

Disk space issues are common on CI/CD servers because build systems generate large numbers of artifacts, logs, temporary files, and container images. Troubleshooting involves identifying the cause, cleaning up unnecessary files, and implementing monitoring or automation to prevent recurrence.

---

### Symptoms of Disk Space Issues

Common indicators of disk space problems include:

- Builds failing with errors such as **“No space left on device”**
- Jenkins or GitLab Runner jobs failing unexpectedly
- Log files not being written
- High disk usage on partitions like `/`, `/var`, or CI/CD workspace directories

---

### Check Disk Usage

The first step is to examine the overall disk usage.

Check disk usage of mounted filesystems:

```
df -h
```

Explanation:

- `-h` displays sizes in human-readable format
- Look for partitions nearing **100% usage**

---

### Check Inode Usage

Sometimes disk space may still be available, but the system runs out of **inodes**, which prevents new files from being created.

Check inode usage:

```
df -i
```

If inodes are exhausted, you may still see **“No space left on device”** even though disk space appears available.

---

### Identify Large Files and Directories

To determine what is consuming disk space, examine directory sizes.

Check disk usage of top-level directories:

```
du -sh /*
```

Check directories commonly used by CI/CD tools such as logs or workspaces:

```
du -sh /var/*
```

---

### Find Largest Files and Directories Recursively

To locate the largest items on the system:

```
du -ah / | sort -rh | head -n 20
```

Explanation:

- `du -ah` lists sizes of files and directories
- `sort -rh` sorts results in descending order
- `head -n 20` shows the top 20 largest items

---

### Find Large Log Files

Log files are often a major contributor to disk usage.

Search for large log files:

```
find /var/log -type f -exec du -h {} + | sort -rh | head -n 10
```

This lists the largest log files in `/var/log`.

---

### Clean Up Disk Space

Once large files or directories are identified, you can free space by removing unnecessary data.

---

### Clean Package Cache

Package managers often cache downloaded packages.

Debian/Ubuntu:

```
sudo apt clean
```

RHEL/CentOS:

```
sudo yum clean all
```

---

### Remove Old Kernels

Old kernels may consume disk space.

```
sudo apt autoremove
```

---

### Clean Docker Images and Containers

CI/CD pipelines frequently use containers, which can accumulate unused images and containers.

Clean Docker resources:

```
docker system prune -af
```

This removes:

- unused images
- stopped containers
- unused networks
- build cache

---

### Remove Old CI/CD Artifacts

Old builds and artifacts often consume significant disk space.

Example for Jenkins:

Go to:

```
Manage Jenkins → Configure System → Build Discarder
```

Alternatively, manually delete old build directories:

```
rm -rf /var/lib/jenkins/jobs/<job_name>/builds/*
```

---

### Log Rotation

Ensure log files are rotated and compressed automatically.

Configuration files:

```
/etc/logrotate.conf
/etc/logrotate.d/*
```

Proper log rotation prevents log files from growing indefinitely.

---

### Monitor Disk Usage

Monitoring helps detect disk issues before they cause failures.

---

### Set Up Disk Alerts

Use monitoring tools such as:

- Nagios
- Prometheus
- Grafana

These tools can trigger alerts when disk usage exceeds a defined threshold.

---

### Automate Cleanup with Cron

You can schedule cleanup scripts using cron.

Example: Delete files older than 30 days

```
find /var/lib/jenkins/jobs/*/builds/ -type f -mtime +30 -exec rm -f {} \;
```

This command removes old build artifacts automatically.

---

### Common Causes of Disk Space Issues on CI/CD Servers

Typical reasons include:

- Old builds and artifacts not being cleaned
- Accumulation of large Docker images and containers
- Log files growing without rotation
- Temporary files from failed builds

---

### Tricky Interview Questions

Why does the system show free disk space but commands like `touch` fail with **“No space left”**?

This is usually due to **inode exhaustion**. Check with:

```
df -i
```

---

How can you prevent Jenkins from filling the disk?

- Configure **build discarder**
- Regularly clean old workspaces
- Monitor disk usage with alerts

---

How can Docker images be cleaned safely?

Use commands such as:

```
docker image prune
```

or

```
docker system prune -af
```

Ensure that images currently in use are not removed.

---

How can disk cleanup be automated in CI/CD environments?

Automation methods include:

- Cron-based cleanup scripts
- Jenkins post-build cleanup plugins
- Log rotation for log management

---

### Interview Summary

To troubleshoot disk space issues on a CI/CD server, administrators typically check disk usage using tools like `df` and `du`, identify large files or directories, clean caches and old build artifacts, manage Docker resources, and implement monitoring or automated cleanup strategies.

### Question
How do you display all installed services with their statuses in Linux?

### Answer

In modern Linux systems that use **systemd** (such as Ubuntu, Debian, CentOS 7+, Fedora), the `systemctl` command is used to **list, manage, and check the status of services**.

---

### Basic Command to List Services

```
systemctl list-units --type=service
```

Explanation:

- `list-units` → Lists all systemd units currently loaded
- `--type=service` → Filters only **services** (ignores mounts, sockets, etc.)

This command shows **currently loaded services**, including running and some inactive ones.

---

### Sample Output

```
UNIT                               LOAD   ACTIVE   SUB     DESCRIPTION
cron.service                        loaded active   running Regular background program processing daemon
dbus.service                        loaded active   running D-Bus System Message Bus
nginx.service                       loaded inactive dead    A high performance web server
```

---

### Column Explanation

| Column | Meaning |
|---|---|
| UNIT | Name of the service |
| LOAD | Whether systemd loaded the service configuration (`loaded`, `not-found`) |
| ACTIVE | High-level state (`active`, `inactive`, `failed`) |
| SUB | Detailed state (`running`, `exited`, `dead`, etc.) |
| DESCRIPTION | Brief description of the service |

---

### Alternative Commands

---

#### List All Services (Including Inactive)

```
systemctl list-unit-files --type=service
```

This command shows all installed services along with their **startup state**, such as:

- enabled
- disabled
- static
- masked

Useful for understanding which services start at boot.

---

#### Check Status of a Specific Service

```
systemctl status nginx.service
```

Displays detailed information:

- current status
- logs
- process ID (PID)
- recent activity

---

#### List Only Active Services

```
systemctl list-units --type=service --state=active
```

Shows only services that are currently running.

---

#### List Only Failed Services

```
systemctl --failed
```

Displays services that have failed, useful for troubleshooting.

---

### Tricky Interview Questions

---

#### How do you see all services, not just running ones?

```
systemctl list-unit-files --type=service
```

This shows all services, including **inactive, disabled, and masked** ones.

---

#### What is the difference between ACTIVE and SUB?

| Field | Meaning |
|---|---|
| ACTIVE | High-level state (active, inactive, failed) |
| SUB | Detailed state (running, exited, dead, waiting) |

---

#### How do you filter services by status?

Example: show failed services

```
systemctl list-units --type=service --state=failed
```

---

#### How do you check if a service starts at boot?

```
systemctl is-enabled nginx.service
```

Possible outputs:

- enabled
- disabled
- static
- masked

---

### Interview Summary

To display all services and their statuses in Linux, the primary command is `systemctl list-units --type=service`. For a complete view including startup configuration, `systemctl list-unit-files --type=service` is used. These commands help monitor, manage, and troubleshoot system services effectively.

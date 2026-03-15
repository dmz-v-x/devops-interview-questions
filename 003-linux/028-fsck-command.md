### Question
Explain the role of the `fsck` command.

### Answer

The `fsck` command in Linux stands for **File System Consistency Check**.  
It is used to **check and repair file systems for errors**.

`fsck` scans a filesystem for inconsistencies and optionally repairs them. It is similar to the **`chkdsk` utility in Windows**, which also checks and fixes disk-related issues.

---

### What is `fsck`?

`fsck` (File System Consistency Check):

- Verifies the integrity of a filesystem
- Detects filesystem corruption
- Repairs errors if possible

It is commonly used when the system experiences disk-related issues or improper shutdowns.

---

### Why `fsck` is Needed

File system corruption can occur due to several reasons, including:

- Sudden power failure
- Improper system shutdown
- Hardware problems such as bad sectors
- System crashes

When corruption occurs, the filesystem may contain inconsistencies. `fsck` scans the filesystem to detect issues such as:

- Inode inconsistencies
- Corrupted directory entries
- Lost clusters
- Bad blocks

These issues can prevent files from being accessed correctly or may cause system instability.

---

### How `fsck` Works

The `fsck` command performs several operations:

1. Checks the filesystem structure for inconsistencies
2. Reports detected errors
3. Optionally fixes errors either interactively or automatically

The repair process may prompt the user for confirmation before fixing detected problems.

---

### Basic Syntax

```
fsck [options] <filesystem>
```

Where:

- `<filesystem>` refers to a device such as `/dev/sda1`
- It may sometimes refer to a mount point like `/`

Example device names:

```
/dev/sda1
/dev/sdb2
```

---

### Common Usage Examples

#### Check a filesystem

```
sudo fsck /dev/sda1
```

This checks the filesystem and **prompts the user interactively** to confirm repairs.

---

#### Automatically fix errors

```
sudo fsck -y /dev/sda1
```

Option used:

- `-y` automatically answers **yes** to all repair prompts.

This automatically fixes detected issues.

---

#### Force a filesystem check

```
sudo fsck -f /dev/sda1
```

Option used:

- `-f` forces a filesystem check even if the system believes the filesystem is clean.

---

#### Check all filesystems

```
sudo fsck -A
```

Option used:

- `-A` checks **all filesystems listed in `/etc/fstab`**.

---

### Important Notes

Running `fsck` incorrectly can damage the filesystem.

Important rule:

**Do not run `fsck` on a mounted filesystem (especially read-write).**

This can cause **data corruption** because the filesystem may be actively changing while the check runs.

Best practice:

- Run `fsck` in **single-user mode**
- Or use a **live CD / live USB environment**
- Especially when checking the **root filesystem (`/`)**

---

### Related Options

| Option | Description |
|------|-------------|
| `-y` | Automatically repair detected errors |
| `-n` | Do not repair; only report errors |
| `-f` | Force check even if filesystem appears clean |
| `-A` | Check all filesystems listed in `/etc/fstab` |
| `-C` | Show progress during filesystem check |

---

### Tricky Interview Questions

Can you run `fsck` on a mounted filesystem?

Generally **no**, especially if the filesystem is mounted **read-write**.  
Doing so may corrupt data. Instead, run `fsck` from **single-user mode or a live environment**.

---

What is the difference between `fsck` and `e2fsck`?

| Command | Purpose |
|------|---------|
| `fsck` | Generic command that automatically detects filesystem type |
| `e2fsck` | Specifically used for `ext2`, `ext3`, and `ext4` filesystems |

---

How can you check a filesystem without making changes?

```
sudo fsck -n /dev/sda1
```

Option `-n` tells `fsck` to **report errors without modifying the filesystem**.

---

What types of errors can `fsck` fix?

`fsck` can repair issues such as:

- inode errors
- corrupted directory entries
- lost clusters
- bad blocks

---

### Interview Summary

The `fsck` command checks and repairs filesystem inconsistencies in Linux. It is typically used after system crashes, power failures, or disk errors to ensure filesystem integrity and restore normal system operation.

### Question
How do you mount and unmount a file system in Linux?

### Answer

In Linux, all files and storage devices are organized under a **single directory tree**. Unlike Windows, which uses drive letters (C:, D:, etc.), Linux requires storage devices to be **mounted to a directory called a mount point** before they can be accessed.

Mounting attaches a storage device to the filesystem, while unmounting safely detaches it.

---

### Understanding Mounting in Linux

- Linux uses a **single directory hierarchy**.
- Devices such as **hard drives, USB drives, ISO images, or network shares** must be mounted to a directory.
- The directory where the device is attached is called a **mount point**.
- Unmounting safely disconnects the device from the filesystem.

---

### Mounting a File System

#### Syntax

    mount [options] <device> <mount_point>

Explanation:

- `<device>` → storage device or partition (e.g., `/dev/sdb1`)
- `<mount_point>` → directory where the device will be attached (must already exist)

---

### Basic Example

Create a mount point:

    sudo mkdir -p /mnt/usb

Mount the device:

    sudo mount /dev/sdb1 /mnt/usb

Explanation:

- `/dev/sdb1` → USB drive or partition
- `/mnt/usb` → mount point

Check mounted devices:

    mount | grep /mnt/usb

or

    df -h

---

### Mounting with File System Type

You can specify the filesystem type using the `-t` option.

Example:

    sudo mount -t ext4 /dev/sdb1 /mnt/usb

Examples of filesystem types:

- ext4
- xfs
- ntfs
- vfat

---

### Mount Options

Mount options control how the filesystem behaves.

Example:

    sudo mount -o rw,noexec,nodev /dev/sdb1 /mnt/usb

Common mount options:

| Option | Description |
|------|-------------|
| rw | Read and write access |
| ro | Read-only access |
| noexec | Prevent execution of files |
| nodev | Ignore device files |
| nosuid | Ignore SUID/SGID bits |

---

### Mount Automatically at Boot (`/etc/fstab`)

To automatically mount a filesystem during system startup, add an entry to the `/etc/fstab` file.

Example entry:

    /dev/sdb1   /mnt/usb   ext4   defaults   0   2

Explanation:

| Field | Meaning |
|------|---------|
| `/dev/sdb1` | Device |
| `/mnt/usb` | Mount point |
| `ext4` | Filesystem type |
| `defaults` | Default mount options |
| `0` | Dump backup option |
| `2` | Filesystem check order |

Apply the configuration without rebooting:

    sudo mount -a

---

### Unmounting a File System

Unmounting detaches the filesystem safely.

#### Syntax

    umount <device_or_mount_point>

Examples:

    sudo umount /mnt/usb
    sudo umount /dev/sdb1

---

### Troubleshooting Unmounting

If you see **device busy** errors, it means a process is still using the filesystem.

Find processes using the mount point:

    sudo lsof /mnt/usb

or

    sudo fuser -m /mnt/usb

Force unmount options:

Lazy unmount:

    sudo umount -l /mnt/usb

Force unmount (mostly for network filesystems):

    sudo umount -f /mnt/usb

---

### Mounting Special File Systems

Mount an ISO image:

    sudo mount -o loop ubuntu.iso /mnt/iso

Mount a Network File System (NFS):

    sudo mount -t nfs 192.168.1.100:/shared /mnt/nfs

Mount a Windows/NTFS partition:

    sudo mount -t ntfs-3g /dev/sdb1 /mnt/usb

---

### Checking Mounted File Systems

Several commands help verify mounted devices.

List mounted filesystems:

    mount

Show disk usage for mounted partitions:

    df -h

Display devices and mount points:

    lsblk

Show a detailed mount tree:

    findmnt

---

### Tricky Interview Questions

How do you mount a filesystem as read-only?

    sudo mount -o ro /dev/sdb1 /mnt/usb

---

How do you mount an ISO image without burning it?

    sudo mount -o loop ubuntu.iso /mnt/iso

---

How do you safely unmount a busy device?

Use `lsof` or `fuser` to identify processes using it, then unmount.

Example:

    sudo lsof /mnt/usb

Or perform a lazy unmount:

    sudo umount -l /mnt/usb

---

How do you mount a partition permanently?

Add the configuration to `/etc/fstab` and run:

    sudo mount -a

---

### Interview Summary

Mounting in Linux attaches a storage device to a directory so it can be accessed through the filesystem. This is done using the `mount` command, while `umount` safely detaches it. Devices can also be configured to mount automatically during boot using the `/etc/fstab` file.

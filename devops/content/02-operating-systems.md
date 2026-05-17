# Operating Systems & Linux

## Why OS Knowledge Matters for DevOps

Every application you deploy, every container you orchestrate, and every server you provision runs on top of an operating system. A DevOps engineer who lacks OS fundamentals is essentially building on a foundation they do not understand. When a production service starts consuming excessive memory, when disk I/O becomes a bottleneck, or when a process mysteriously dies at 3 AM, the difference between a quick resolution and hours of flailing comes down to how well you understand what is happening beneath your application layer.

OS knowledge is not optional background reading -- it is a core competency. You need it to write efficient Dockerfiles, tune kernel parameters for high-throughput networking, debug permission errors in CI/CD pipelines, configure storage for databases, and reason about why your autoscaling policy is not behaving as expected.

---

## OS Fundamentals

### Processes and Threads

A **process** is an instance of a running program. Each process has its own address space, file descriptors, and execution context. The OS kernel manages processes through a scheduler that decides which process gets CPU time and for how long.

Key concepts:
- **PID (Process ID)**: A unique numeric identifier assigned to each process.
- **Parent-child relationships**: Every process (except PID 1, the init process) is spawned by a parent. When a parent dies without waiting for its children, those children become orphans and are adopted by init.
- **Process states**: Running, sleeping (waiting for I/O or a signal), stopped (paused by a signal), and zombie (finished execution but its exit status has not been collected by the parent).
- **Signals**: Mechanisms for inter-process communication. Common ones include SIGTERM (polite shutdown request), SIGKILL (forceful termination, cannot be caught), SIGHUP (hangup, often used to trigger config reloads), and SIGINT (interrupt, what Ctrl+C sends).

A **thread** is a lightweight unit of execution within a process. Threads within the same process share memory and file descriptors, which makes communication between them fast but also introduces the complexity of race conditions and the need for synchronization primitives like mutexes and semaphores.

For DevOps, understanding processes and threads matters when you are analyzing resource usage, configuring process limits, or debugging why a container is being OOM-killed.

### Memory Management

The OS provides each process with a virtual address space, creating the illusion that each process has access to the entire memory range. The kernel's memory management unit (MMU) translates virtual addresses to physical addresses.

Key concepts:
- **Virtual memory**: Allows the system to use disk space (swap) as an extension of RAM. When physical memory is full, the kernel moves less-used memory pages to swap. This prevents out-of-memory crashes but causes severe performance degradation.
- **Pages**: Memory is divided into fixed-size blocks called pages (typically 4 KB). The kernel tracks which pages are in physical RAM and which are on disk.
- **OOM Killer**: When the system runs critically low on memory, the Linux OOM killer selects and terminates processes to free up RAM. It assigns an OOM score to each process, and the one with the highest score gets killed first. Understanding this is critical when running memory-intensive workloads.
- **Cgroups (Control Groups)**: Linux feature that limits and isolates resource usage (CPU, memory, disk I/O) for groups of processes. Containers rely heavily on cgroups to enforce resource limits.

### File Systems

A file system defines how data is organized, stored, and retrieved on a storage device.

Common Linux file systems:
- **ext4**: The default for most Linux distributions. Journaling file system that provides a good balance of performance and reliability.
- **XFS**: High-performance file system well-suited for large files and parallel I/O. Default on RHEL-based distributions.
- **Btrfs**: Copy-on-write file system with built-in support for snapshots, compression, and RAID. Used as default on some SUSE configurations.
- **tmpfs**: A file system that lives entirely in RAM. Used for `/tmp` and `/run` on many systems. Fast but volatile.
- **overlayfs**: A union file system that layers multiple directories on top of each other. Docker uses this as its default storage driver.

### I/O (Input/Output)

Everything in Linux is treated as a file -- regular files, directories, devices, sockets, and pipes all present a file-like interface. I/O operations are how processes interact with these resources.

Key concepts:
- **File descriptors**: Integer handles that processes use to reference open files. FD 0 is stdin, FD 1 is stdout, FD 2 is stderr.
- **Blocking vs non-blocking I/O**: Blocking I/O makes the calling process wait until the operation completes. Non-blocking I/O returns immediately, allowing the process to do other work.
- **Buffering**: The kernel and standard library buffer I/O operations to reduce the number of expensive system calls. This is why output sometimes does not appear immediately when piped.
- **I/O schedulers**: The kernel uses schedulers (e.g., `mq-deadline`, `bfq`, `none`) to determine the order in which disk I/O requests are serviced. Choosing the right scheduler matters for database and storage-heavy workloads.

---

## Linux Distributions

### Ubuntu / Debian Family

Debian is one of the oldest and most stable distributions. Ubuntu is built on top of Debian and adds more frequent releases, better hardware support out of the box, and a larger ecosystem of PPAs (Personal Package Archives).

- **Package manager**: `apt` (Advanced Package Tool), with `.deb` packages.
- **Release model**: Debian favors stability with infrequent releases. Ubuntu follows a six-month release cycle with LTS (Long Term Support) versions every two years, supported for five years.
- **Common use**: Ubuntu dominates cloud server deployments. It is the default image on most cloud providers and has the largest community for troubleshooting.

### RHEL / CentOS / Rocky / AlmaLinux Family

Red Hat Enterprise Linux (RHEL) is a commercial distribution focused on enterprise stability and long-term support. CentOS was its free community rebuild until Red Hat shifted it to CentOS Stream (a rolling preview of RHEL). Rocky Linux and AlmaLinux emerged as direct RHEL-compatible replacements.

- **Package manager**: `yum` (legacy) or `dnf` (modern replacement), with `.rpm` packages.
- **Release model**: Major versions are supported for 10+ years. Emphasis on binary compatibility and certification.
- **Common use**: Enterprise data centers, regulated industries, and environments that require vendor support contracts. Many production Kubernetes clusters run on RHEL-family distributions.

### SUSE / openSUSE

SUSE Linux Enterprise Server (SLES) is another enterprise-grade distribution. openSUSE Leap is its community counterpart, while openSUSE Tumbleweed is a rolling-release variant.

- **Package manager**: `zypper`, with `.rpm` packages.
- **Distinguishing feature**: YaST (Yet another Setup Tool), a comprehensive system configuration tool. Strong presence in European enterprise environments and SAP deployments.

### Arch Linux

A minimalist, rolling-release distribution that gives you full control over what gets installed. Not typically used in production servers but highly valued for learning because nothing is abstracted away.

- **Package manager**: `pacman`, with the AUR (Arch User Repository) providing community-maintained packages.
- **Philosophy**: Simplicity, transparency, and user-centricity. The Arch Wiki is widely regarded as one of the best Linux documentation resources, useful even for users of other distributions.

---

## Virtualization

### Types of Virtualization

**Hardware virtualization (full virtualization)**: A hypervisor creates complete virtual machines, each with its own virtualized hardware (CPU, RAM, network interfaces, storage). The guest OS runs unmodified, unaware it is virtualized.

**OS-level virtualization (containerization)**: Instead of virtualizing hardware, the host kernel is shared among isolated user-space instances (containers). Each container has its own filesystem, process tree, and network stack, but they all share the same kernel. This is what Docker and LXC use.

**Application-level virtualization**: A runtime environment abstracts away the underlying OS. The Java Virtual Machine (JVM) is a classic example -- Java bytecode runs on any platform with a compatible JVM.

### Hypervisors: Type 1 vs Type 2

**Type 1 (bare-metal) hypervisors** run directly on the physical hardware, with no host OS underneath. They manage guest operating systems directly.
- Examples: VMware ESXi, Microsoft Hyper-V, KVM (technically runs as a kernel module, blurring the line), Xen.
- Use case: Data center virtualization, cloud providers. AWS EC2 instances run on a customized version of KVM (Nitro).

**Type 2 (hosted) hypervisors** run as applications on top of a host operating system.
- Examples: VirtualBox, VMware Workstation, Parallels Desktop.
- Use case: Development environments, testing, running a different OS on your laptop.

### VMs vs Containers

| Aspect | Virtual Machines | Containers |
|---|---|---|
| Isolation | Full hardware-level isolation | Process-level isolation via namespaces and cgroups |
| Overhead | Each VM runs its own kernel and OS; significant resource overhead | Share the host kernel; lightweight, start in milliseconds |
| Size | Typically gigabytes (full OS image) | Typically megabytes (application and dependencies only) |
| Boot time | Minutes | Seconds or less |
| Security boundary | Strong -- separate kernels mean a guest exploit is unlikely to affect the host | Weaker -- a kernel vulnerability can potentially escape the container |
| Use case | Running different OS types, strong isolation requirements, legacy apps | Microservices, CI/CD, rapid scaling, development environments |

In practice, VMs and containers are not mutually exclusive. Many production environments run containers inside VMs to get both the density benefits of containers and the security isolation of VMs (e.g., Kubernetes nodes running as VMs on a cloud provider).

---

## Key Linux Concepts

### The Kernel

The kernel is the core of the operating system. It manages hardware resources, enforces security boundaries, and provides system calls that applications use to interact with hardware. The Linux kernel is monolithic (all core functionality runs in kernel space) but supports loadable modules that can be inserted and removed at runtime.

DevOps-relevant kernel tuning:
- `sysctl` parameters for networking (e.g., `net.core.somaxconn` for connection backlog, `net.ipv4.ip_forward` for routing).
- File descriptor limits (`fs.file-max` and per-process limits via `ulimit`).
- Virtual memory behavior (`vm.swappiness` controls how aggressively the kernel swaps).

### The Shell

The shell is the command-line interpreter that sits between the user and the kernel. It reads commands, interprets them, and asks the kernel to execute them.

Common shells:
- **bash**: The default on most Linux distributions. POSIX-compatible with extensions.
- **zsh**: Default on macOS. Offers better autocompletion, globbing, and plugin ecosystem (Oh My Zsh).
- **sh**: The original Bourne shell. Scripts written for `/bin/sh` are the most portable.
- **fish**: User-friendly with syntax highlighting and autosuggestions out of the box, but not POSIX-compatible.

### Filesystem Hierarchy Standard (FHS)

Linux follows a standardized directory structure:

- `/` -- Root of the entire filesystem.
- `/bin` -- Essential user binaries (ls, cp, cat). On modern systems, often a symlink to `/usr/bin`.
- `/sbin` -- System administration binaries (iptables, fdisk).
- `/etc` -- Configuration files for the system and installed services.
- `/home` -- User home directories.
- `/var` -- Variable data: logs (`/var/log`), spool files, temporary data that persists across reboots.
- `/tmp` -- Temporary files, typically cleared on reboot.
- `/usr` -- User programs, libraries, and documentation. `/usr/local` is for locally compiled software.
- `/opt` -- Optional/third-party software packages.
- `/proc` -- Virtual filesystem exposing kernel and process information as files.
- `/sys` -- Virtual filesystem for kernel objects (devices, drivers, modules).
- `/dev` -- Device files (e.g., `/dev/sda` for the first disk, `/dev/null` for the bit bucket).

### Permissions, Users, and Groups

Linux uses a permission model based on three categories: **owner**, **group**, and **others**. Each category can have **read (r=4)**, **write (w=2)**, and **execute (x=1)** permissions.

```
-rwxr-xr-- 1 deploy webteam 4096 Mar 10 14:22 deploy.sh
```
This file is owned by user `deploy` and group `webteam`. The owner can read, write, and execute. Group members can read and execute. Others can only read.

Important commands:
- `chmod 755 file` -- Set permissions using octal notation.
- `chown user:group file` -- Change ownership.
- `umask 022` -- Set default permissions for new files.

Special permissions:
- **SUID (Set User ID)**: When set on an executable, it runs with the permissions of the file owner, not the user who executed it. Example: `/usr/bin/passwd` runs as root so users can change their own passwords.
- **SGID (Set Group ID)**: On a directory, new files created inside inherit the directory's group.
- **Sticky bit**: On a directory, only the file owner can delete their own files. Used on `/tmp`.

---

## Package Management

### apt (Debian/Ubuntu)

```bash
apt update                    # Refresh package index from repositories
apt upgrade                   # Upgrade all installed packages
apt install nginx             # Install a package
apt remove nginx              # Remove a package (keep config files)
apt purge nginx               # Remove a package and its config files
apt search "web server"       # Search for packages
apt show nginx                # Display package details
apt autoremove                # Remove unused dependencies
```

Repositories are configured in `/etc/apt/sources.list` and files under `/etc/apt/sources.list.d/`.

### yum / dnf (RHEL/CentOS/Fedora)

`dnf` is the modern replacement for `yum`. The command syntax is largely compatible.

```bash
dnf check-update              # Check for available updates
dnf upgrade                   # Upgrade all packages
dnf install httpd             # Install a package
dnf remove httpd              # Remove a package
dnf search "web server"       # Search for packages
dnf info httpd                # Display package details
dnf autoremove                # Remove unused dependencies
dnf list installed            # List all installed packages
```

Repositories are configured in `/etc/yum.repos.d/`.

### pacman (Arch Linux)

```bash
pacman -Syu                   # Sync databases and upgrade all packages
pacman -S nginx               # Install a package
pacman -R nginx               # Remove a package
pacman -Rs nginx              # Remove a package and its unused dependencies
pacman -Ss "web server"       # Search for packages
pacman -Qi nginx              # Display info about an installed package
pacman -Ql nginx              # List files owned by a package
```

---

## Systemd and Service Management

Systemd is the init system and service manager used by nearly all modern Linux distributions. It replaced older init systems (SysVinit, Upstart) and manages the entire lifecycle of system services, from boot to shutdown.

### Core Concepts

- **Units**: The basic objects that systemd manages. The most common types are:
  - `.service` -- Daemons and background services.
  - `.timer` -- Scheduled tasks (replacement for cron).
  - `.socket` -- Socket-based activation.
  - `.mount` -- Filesystem mount points.
  - `.target` -- Groups of units (analogous to runlevels).

- **Unit files** are stored in `/etc/systemd/system/` (administrator overrides) and `/usr/lib/systemd/system/` (package defaults).

### Common systemctl Commands

```bash
systemctl start nginx         # Start a service
systemctl stop nginx          # Stop a service
systemctl restart nginx       # Restart a service
systemctl reload nginx        # Reload configuration without full restart
systemctl enable nginx        # Start service automatically at boot
systemctl disable nginx       # Do not start at boot
systemctl status nginx        # Show service status and recent log entries
systemctl is-active nginx     # Check if a service is running
systemctl is-enabled nginx    # Check if a service is enabled at boot
systemctl list-units --type=service  # List all loaded services
systemctl daemon-reload       # Reload unit file changes
```

### Writing a Custom Service Unit

```ini
[Unit]
Description=My Application Server
After=network.target postgresql.service
Requires=postgresql.service

[Service]
Type=simple
User=appuser
Group=appuser
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/bin/server --config /etc/myapp/config.yaml
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure
RestartSec=5
StandardOutput=journal
StandardError=journal
LimitNOFILE=65536

[Install]
WantedBy=multi-user.target
```

Key directives explained:
- `After` / `Requires`: Dependency ordering. The service starts after the listed units.
- `Type=simple`: Systemd considers the service started as soon as the main process is forked.
- `Restart=on-failure`: Automatically restart if the process exits with a non-zero code.
- `RestartSec=5`: Wait 5 seconds between restart attempts.
- `LimitNOFILE`: Set the maximum number of open file descriptors.
- `WantedBy=multi-user.target`: This service is part of the normal multi-user boot target.

### Journalctl for Logs

Systemd captures all service output in the journal, which is queried with `journalctl`.

```bash
journalctl -u nginx           # Logs for a specific service
journalctl -u nginx --since "1 hour ago"  # Logs from the last hour
journalctl -u nginx -f        # Follow logs in real time (like tail -f)
journalctl -b                 # All logs from the current boot
journalctl -p err             # Only error-level messages and above
journalctl --disk-usage       # Show how much disk space the journal uses
journalctl --vacuum-size=500M # Trim the journal to 500 MB
```

---

## Summary

Operating system knowledge is foundational for DevOps. You do not need to be a kernel developer, but you must understand how processes consume resources, how memory and storage are managed, how permissions control access, and how services are configured and monitored. This knowledge directly translates into your ability to debug production issues, write efficient automation, and build infrastructure that behaves predictably under load.

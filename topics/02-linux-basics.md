# Linux Mastery for DevOps Engineers

This document provides a comprehensive, in-depth guide to Linux skills essential for DevOps.  
Linux forms the foundation for servers, cloud instances, containers, CI/CD pipelines, Kubernetes nodes, and automation. Without strong Linux proficiency, working with Docker, Kubernetes, Ansible, Terraform, and monitoring tools becomes significantly harder.

Master these concepts through hands-on practice on a Ubuntu VM (recommended for beginners).

## 1. Linux File System Hierarchy (FHS)

Linux follows a single-root hierarchical structure defined by the **Filesystem Hierarchy Standard (FHS)**. Everything starts from the root directory `/`.

### Key Directories and Their Purposes

| Directory     | Purpose                                                                 | DevOps Relevance                                      |
|---------------|-------------------------------------------------------------------------|-------------------------------------------------------|
| `/`           | Root of the entire filesystem                                           | All paths are relative to this                        |
| `/bin`        | Essential binary executables (basic commands)                           | Core commands available in single-user mode           |
| `/sbin`       | System binaries (admin commands)                                        | Tools like `ifconfig`, `reboot`                       |
| `/etc`        | Host-specific system configuration files                                | nginx configs, sshd_config, fstab, sudoers            |
| `/var`        | Variable data (logs, spools, web content)                               | `/var/log/` (logs), `/var/www/html/` (web files)      |
| `/home`       | User home directories                                                   | Where you work as a normal user                       |
| `/tmp`        | Temporary files (cleared on reboot)                                     | Safe place for scripts and temp data                  |
| `/usr`        | User programs, libraries, and data                                      | Installed software (`/usr/bin`, `/usr/lib`)           |
| `/opt`        | Optional third-party or custom software                                 | Some applications or tools installed here             |
| `/boot`       | Bootloader and kernel files                                             | Kernel images, GRUB config                            |
| `/proc`       | Virtual filesystem with process and system information                  | Live data: CPU, memory, network (e.g., `/proc/meminfo`) |
| `/dev`        | Device files                                                            | Hardware devices represented as files                 |
| `/mnt` / `/media` | Mount points for external filesystems                                | Temporary mounts of drives or network shares          |

**Tip**: Use `tree -L 2 /` (install with `sudo apt install tree`) to explore the structure.

## 2. Essential Commands

### Navigation and File Management
- `pwd` — Print working directory
- `ls -la` — List all files with details (including hidden)
- `cd /path` — Change directory (`cd \~` for home, `cd -` for previous)
- `mkdir -p dir1/dir2` — Create nested directories
- `cp -r source dest` — Recursive copy
- `mv old new` — Move or rename
- `rm -rf dir` — Remove recursively (use with caution; consider `rm -i` for safety)
- `touch file.txt` — Create empty file or update timestamp
- `cat`, `less`, `more` — View file content
- `tail -f /var/log/syslog` — Follow log file in real-time
- `head -n 20 file` — Show first 20 lines

### Text Processing and Search
- `grep "error" app.log` — Search for text
- `grep -r "pattern" /path` — Recursive search
- `find /var -name "*.log"` — Find files by name
- `locate filename` — Fast search (requires updated database)

### System Information
- `uname -a` — Kernel and system info
- `cat /etc/os-release` — Distribution details
- `df -h` — Disk usage (human readable)
- `free -h` — Memory usage
- `du -sh /path` — Directory size
- `top` / `htop` — Real-time process viewer (install htop if needed)
- `uptime` — System uptime and load

## 3. File Permissions and Ownership

Permissions are displayed as: `drwxr-xr-x` (type, owner, group, others).

Numeric values:
- Read (r) = 4
- Write (w) = 2
- Execute (x) = 1

Common combinations:
- `644` → `rw-r--r--` (files: owner edit, others read)
- `755` → `rwxr-xr-x` (directories and scripts)
- `600` → `rw-------` (private files)

Commands:
```bash
ls -l                  # View permissions
chmod 755 script.sh
chmod +x script.sh     # Make executable
chown user:group file
chown -R www-data:www-data /var/www/html   # Recursive
```

### 4. Process and Service Management  

Process management is one of the most frequently used skills in DevOps. You will regularly check running services, restart them, view resource usage, and troubleshoot issues.

#### Key Concepts
- **Processes**: Running instances of programs
- **Services**: Long-running background processes managed by systemd (the modern init system on Ubuntu)
- **Killing processes**: Graceful vs force kill

#### Important Commands

**Viewing Processes**
```bash
ps aux                  # Show all running processes with details
ps aux | grep nginx     # Filter for a specific process
top                     # Interactive real-time process viewer
htop                    # Better colored version (install with: sudo apt install htop)

# Systemd (modern service manager)
systemctl status nginx
systemctl start nginx
systemctl restart nginx
systemctl enable nginx   # Auto-start on boot
systemctl disable nginx
journalctl -u nginx -f   # Follow service logs
```

## **Installation & Package Management
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install nginx git curl vim -y
sudo apt remove package_name
sudo apt autoremove        # Clean unused dependencies
```

## **Networking and DNS  
```bash
ip addr show            # Show IP addresses and interfaces
ping 8.8.8.8
curl -I https://example.com
ss -tlnp                # Listening ports and processes (replacement for netstat)
dig example.com         # DNS lookup
traceroute example.com
```
## **Firewall  

```bash
# Firewall (ufw - Uncomplicated Firewall)
sudo ufw status
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

## ** User & Permission Management

```bash
whoami
id
sudo -i                 # Become root temporarily
sudo su -               # Full root shell
groups
usermod -aG sudo username   # Add user to sudo group
```
## ** Logs & Troubleshooting  

```bash
journalctl -u service_name
journalctl -u nginx --since "1 hour ago"
tail -f /var/log/nginx/error.log
grep "error" /var/log/syslog

```

## ** Memory & Storage Management  

```bash
df -h                   # Filesystem usage
du -sh /path            # Directory usage
lsblk                   # Block devices (disks)
fdisk -l                # Partition table (use with caution)
```
**Super User Activity**

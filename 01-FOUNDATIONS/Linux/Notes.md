# Philosophy

- Treat everything as a file
- Small single-purpose programs
- Ability to perform complex tasks
- Configure data in files

# Components

| Component | Description |
|---|---|
| **Kernel** | Core of Linux; manages CPU, memory, processes, devices, and system calls. |
| **Shell** | Interface between the user and kernel. Examples: Bash, Zsh. |
| **File System** | Organizes and stores files/directories using structures like `/`, `/home`, `/etc`, `/var`. |
| **System Utilities** | Commands/tools used to manage and interact with the system, e.g. `ls`, `cp`, `ps`, `chmod`. |
| **System Libraries** | Provide functions that applications use to interact with the kernel. |
| **Applications** | User programs such as text editors, browsers, development tools, and security tools. |

# Architecture

| Layer | Description |
|---|---|
| **Hardware** | CPU, RAM, storage, network devices, etc. |
| **Kernel** | Core of Linux; manages hardware, memory, processes, networking, and file systems. |
| **System Libraries** | Provide standard functions for applications to interact with the kernel. |
| **System Utilities** | Tools and commands for system management, e.g. `ls`, `ps`, `chmod`. |
| **Shell** | Provides a command-line interface between the user and the OS, e.g. Bash. |
| **Applications** | Programs used by the user, such as editors, browsers, and security tools. |

# Important Directories

| Directory | Purpose |
|---|---|
| `/` | Root of the filesystem |
| `/home` | Normal users' home directories |
| `/etc` | Configuration files |
| `/var` | Logs, caches, application data |
| `/usr` | User programs and utilities |
| `/bin` | Essential commands |
| `/sbin` | System administration commands |
| `/proc` | Process/kernel information |
| `/sys` | Kernel/device information |
| `/boot` | Bootloader/kernel files |

# Linux Important Commands

## 1. User & System Information

| Command | Description |
|---|---|
| `who` | Displays who is logged in. |
| `whoami` | Displays the current username. |
| `id` | Displays the user's UID, GID, and group memberships. |
| `hostname` | Displays or sets the hostname of the system. |
| `uname` | Displays operating system/kernel information. |
| `uname -a` | Displays detailed system and kernel information. |
| `env` | Displays environment variables. |
| `echo $PATH` | Displays directories searched for executable commands. |
| `groups` | Displays the groups the current user belongs to. |

## 2. Navigation & File Management

| Command | Description |
|---|---|
| `pwd` | Displays the current working directory. |
| `ls` | Lists directory contents. |
| `ls -la` | Lists all files, including hidden files, with detailed information. |
| `cd` | Changes the current directory. |
| `cd ..` | Moves one directory up. |
| `cd ~` | Moves to the current user's home directory. |
| `cd -` | Returns to the previous directory. |
| `clear` | Clears the terminal screen. |
| `touch` | Creates an empty file. |
| `mkdir` | Creates a directory. |
| `mkdir -p` | Creates directories and required parent directories. |
| `tree` | Displays directory contents recursively as a tree. |
| `mv` | Moves or renames files and directories. |
| `cp` | Copies files. |
| `cp -r` | Copies directories recursively. |
| `rm` | Removes files. |
| `rm -r` | Removes directories recursively. |

## 3. File Searching & Information

| Command | Description |
|---|---|
| `which` | Displays the path of an executable command. |
| `find` | Searches for files and directories in a directory hierarchy. |
| `locate` | Searches for files using a pre-built database. |
| `updatedb` | Updates the database used by `locate`. |
| `file` | Identifies the type of a file. |

## 4. Reading Files

| Command | Description |
|---|---|
| `cat` | Displays or concatenates file contents. |
| `more` | Displays output one screen at a time. |
| `less` | Displays files page-by-page with more features than `more`. |
| `head` | Displays the first 10 lines of a file. |
| `tail` | Displays the last 10 lines of a file. |
| `tail -f` | Continuously displays new content added to a file. |

## 5. Text Searching & Processing

| Command | Description |
|---|---|
| `grep` | Searches for lines matching a specified pattern. |
| `grep -i` | Performs a case-insensitive search. |
| `grep -r` | Searches recursively through directories. |
| `sort` | Sorts lines of text. |
| `uniq` | Removes or counts repeated lines. |
| `cut` | Extracts sections or fields from each line. |
| `tr` | Translates, replaces, or deletes characters. |
| `column` | Formats input into aligned columns. |
| `awk` | Pattern scanning and text-processing language. |
| `sed` | Stream editor used for filtering and transforming text. |
| `wc` | Counts lines, words, and bytes. |

## 6. Networking

| Command | Description |
|---|---|
| `ifconfig` | Displays or configures network interfaces. |
| `ip` | Shows or manipulates network interfaces, routes, and other network information. |
| `ip addr` | Displays IP addresses and network interfaces. |
| `ip route` | Displays the routing table. |
| `netstat` | Displays network connections and network status. |
| `ss` | Displays information about network sockets and connections. |
| `ss -tulnp` | Displays listening TCP/UDP ports and associated processes. |
| `curl` | Transfers data to or from a server and can make HTTP requests. |
| `wget` | Downloads files from HTTP, HTTPS, and FTP servers. |
| `ping` | Tests network connectivity to a host. |
| `nslookup` | Performs DNS lookups. |
| `hostname -I` | Displays the system's IP addresses. |

## 7. Processes

| Command | Description |
|---|---|
| `ps` | Displays a snapshot of running processes. |
| `top` | Displays real-time process and system resource information. |
| `pstree` | Displays processes in a parent-child tree. |
| `pgrep` | Finds the PID of processes matching a name. |
| `pidof` | Displays the PID of a running program. |
| `kill` | Sends a signal to a process. |
| `kill -9` | Forcefully terminates a process. |
| `jobs` | Displays jobs running in the current shell. |
| `bg` | Moves a suspended job to the background. |
| `fg` | Brings a background job to the foreground. |

## 8. Services & Systemd

| Command | Description |
|---|---|
| `systemctl` | Controls systemd services and system state. |
| `systemctl status` | Displays the status of a service. |
| `systemctl start` | Starts a service. |
| `systemctl stop` | Stops a service. |
| `systemctl restart` | Restarts a service. |
| `systemctl enable` | Enables a service to start at boot. |
| `systemctl disable` | Disables a service from starting at boot. |
| `journalctl` | Displays systemd journal logs. |
| `journalctl -u ssh` | Displays logs related to the SSH service. |
| `journalctl -f` | Continuously displays new system logs. |

## 9. Users & Groups

| Command / File | Description |
|---|---|
| `sudo` | Executes a command with elevated or another user's privileges. |
| `sudo -l` | Displays commands the current user is allowed to run with sudo. |
| `su` | Switches to another user. |
| `su -` | Switches user and loads the target user's login environment. |
| `useradd` | Creates a new user. |
| `userdel` | Deletes a user account. |
| `usermod` | Modifies an existing user account. |
| `addgroup` | Creates a new group. |
| `delgroup` | Deletes a group. |
| `passwd` | Changes a user's password. |
| `/etc/passwd` | Stores information about local user accounts. |
| `/etc/group` | Stores information about groups. |
| `/etc/shadow` | Stores password hashes and related password information. |

## 10. Permissions & Ownership

| Command | Description |
|---|---|
| `chmod` | Changes permissions of a file or directory. |
| `chown` | Changes the owner and/or group of a file or directory. |
| `chgrp` | Changes the group ownership of a file or directory. |
| `ls -l` | Displays file permissions and ownership. |
| `chmod 755` | Sets permissions to `rwxr-xr-x`. |
| `chmod 644` | Sets permissions to `rw-r--r--`. |
| `chmod +x` | Adds execute permission to a file. |

## 11. Special Permissions

| Item | Description |
|---|---|
| **SUID** | Allows an executable to run with the permissions of its owner. |
| **SGID** | Allows an executable to run with group permissions and can affect group inheritance on directories. |
| **Sticky Bit** | Restricts deletion of files in shared directories to their owners or privileged users. |

### Finding SUID / SGID Files

```bash
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
```

## 12. Hardware & Devices

| Command | Description |
|---|---|
| `lsblk` | Lists block/storage devices. |
| `lsusb` | Lists connected USB devices. |
| `lspci` | Lists PCI devices. |
| `lsof` | Lists open files and the processes using them. |

## 13. Package Management

| Command | Description |
|---|---|
| `apt` | High-level package management utility for Debian-based systems. |
| `apt update` | Updates package repository information. |
| `apt upgrade` | Upgrades installed packages. |
| `apt install` | Installs a package. |
| `apt remove` | Removes a package. |
| `dpkg` | Low-level Debian package management utility. |
| `dpkg -i` | Installs a `.deb` package. |
| `dpkg -l` | Lists installed Debian packages. |
| `aptitude` | Alternative package management utility. |
| `snap` | Installs, removes, and manages Snap packages. |

## 14. Programming & Version Control

| Command | Description |
|---|---|
| `pip` | Python package manager. |
| `gem` | Ruby package manager. |
| `git` | Distributed version control system. |
| `git clone` | Clones a remote Git repository. |
| `git status` | Displays the current Git repository status. |
| `git log` | Displays commit history. |

## 15. Bash & Environment

| Command | Description |
|---|---|
| `echo` | Displays text or variable values. |
| `echo $USER` | Displays the current username. |
| `echo $HOME` | Displays the current user's home directory. |
| `echo $PATH` | Displays the system PATH. |
| `export` | Sets or exports environment variables. |
| `history` | Displays previously executed commands. |
| `alias` | Creates or displays command aliases. |
| `man` | Displays the manual page for a command. |
| `command --help` | Displays basic help for a command. |

## 16. Pipes & Redirection

| Operator | Description |
|---|---|
| `\|` | Sends the output of one command as input to another command. |
| `>` | Redirects output to a file and overwrites existing content. |
| `>>` | Redirects output to a file and appends to existing content. |
| `2>` | Redirects error output to a file. |
| `2>/dev/null` | Discards error output. |
| `<` | Takes command input from a file. |

## 17. SSH

| Command / Path | Description |
|---|---|
| `ssh` | Connects securely to a remote system. |
| `ssh user@IP` | Connects to a remote system as the specified user. |
| `ssh -p PORT user@IP` | Connects using a custom SSH port. |
| `ssh-keygen` | Generates an SSH key pair. |
| `ssh -i key user@IP` | Connects using a specified private key. |
| `ssh-copy-id` | Copies a public SSH key to an authorized remote account. |
| `~/.ssh/` | Stores user-specific SSH keys and configuration. |
| `~/.ssh/authorized_keys` | Stores public keys authorized to access an account. |
| `/etc/ssh/sshd_config` | SSH server configuration file. |

## 18. File Transfer & Simple Web Server

| Command | Description |
|---|---|
| `curl` | Transfers data from or to a server. |
| `wget` | Downloads files from a server. |
| `python3 -m http.server 8000` | Starts a simple Python HTTP server on TCP port 8000. |

## 19. Pentesting-Important Commands

| Command | Purpose |
|---|---|
| `whoami` | Identify the current user. |
| `id` | Identify UID, GID, and group memberships. |
| `hostname` | Identify the target system's hostname. |
| `uname -a` | Identify OS/kernel information. |
| `sudo -l` | Check available sudo privileges. |
| `ls -la` | Inspect files, hidden files, ownership, and permissions. |
| `ps aux` | Enumerate running processes. |
| `ss -tulnp` | Enumerate listening network ports and processes. |
| `ip addr` | Enumerate network interfaces and IP addresses. |
| `ip route` | Inspect routing information. |
| `find` | Search for interesting files and directories. |
| `grep` | Search configuration files and other text for specific patterns. |
| `find / -perm -4000 -type f 2>/dev/null` | Enumerate SUID files. |
| `cat /etc/passwd` | View local user account information. |
| `ls -l` | Inspect file permissions and ownership. |
| `systemctl` | Enumerate and manage services. |
| `journalctl` | Inspect systemd logs. |
| `ssh` | Connect to an authorized remote Linux system. |

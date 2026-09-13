#  Linux Command Cheat Sheet

This file provides a beginner-friendly reference for essential Linux commands, starting from basic file management to system administration, networking, permissions, and package management.

---

##  1. File & Directory Management

| Command           | Definition / Purpose                                                                        | Example                  |
| :---------------- | :------------------------------------------------------------------------------------------ | :----------------------- |
| `pwd`             | **Print Working Directory:** Displays the current directory you are working in.             | `pwd`                    |
| `ls`              | **List:** Displays files and directories in the current directory.                          | `ls`                     |
| `ls -la`          | Displays detailed information, including hidden files and directories.                      | `ls -la`                 |
| `cd [dir]`        | **Change Directory:** Moves from the current directory to another directory.                | `cd Documents`           |
| `cd ..`           | Moves one level up to the parent directory.                                                 | `cd ..`                  |
| `cd ~`            | Moves to the current user's home directory.                                                 | `cd ~`                   |
| `mkdir [dir]`     | **Make Directory:** Creates a new directory.                                                | `mkdir my_folder`        |
| `rmdir [dir]`     | Removes an empty directory.                                                                 | `rmdir empty_folder`     |
| `rm [file]`       | **Remove:** Deletes a file.                                                                 | `rm file.txt`            |
| `rm -rf [dir]`    | Recursively removes a directory and its contents. `-f` forces removal without confirmation. | `rm -rf my_folder`       |
| `cp [src] [dest]` | **Copy:** Copies a file or directory to another location.                                   | `cp file1.txt file2.txt` |
| `mv [src] [dest]` | **Move/Rename:** Moves or renames a file or directory.                                      | `mv old.txt new.txt`     |
| `touch [file]`    | Creates a new empty file, or updates the timestamp of an existing file.                     | `touch index.html`       |

---

##  2. File Viewing & Editing

| Command                | Definition / Purpose                                      | Example                |
| :--------------------- | :-------------------------------------------------------- | :--------------------- |
| `cat [file]`           | Displays the complete contents of a file in the terminal. | `cat README.md`        |
| `head -n [file]`       | Displays the first specified number of lines of a file.   | `head -n 10 file.txt`  |
| `tail -n [file]`       | Displays the last specified number of lines of a file.    | `tail -n 10 log.txt`   |
| `nano [file]`          | Opens a file in the simple Nano terminal text editor.     | `nano script.sh`       |
| `vim [file]` / `vi`    | Opens a file in the Vim/Vi terminal text editor.          | `vim config.conf`      |
| `grep "[text]" [file]` | Searches for a specific word or pattern inside a file.    | `grep "error" log.txt` |

---

##  3. System Information & Performance

| Command        | Definition / Purpose                                                                                | Example            |
| :------------- | :-------------------------------------------------------------------------------------------------- | :----------------- |
| `uname -a`     | Displays detailed information about the Linux kernel and system.                                    | `uname -a`         |
| `top`          | Displays real-time information about CPU, memory, and running processes.                            | `top`              |
| `htop`         | An interactive and more user-friendly alternative to `top`. It may need to be installed separately. | `htop`             |
| `df -h`        | **Disk Free:** Displays available and used disk space in a human-readable format.                   | `df -h`            |
| `du -sh [dir]` | **Disk Usage:** Shows how much disk space a specific directory is using.                            | `du -sh Downloads` |
| `free -m`      | Displays RAM and swap memory usage in megabytes.                                                    | `free -m`          |
| `uptime`       | Shows how long the system has been running.                                                         | `uptime`           |
| `whoami`       | Displays the username of the currently logged-in user.                                              | `whoami`           |

---

##  4. File Permissions & User Management

| Command                | Definition / Purpose                                                     | Example                    |
| :--------------------- | :----------------------------------------------------------------------- | :------------------------- |
| `sudo [command]`       | Executes a command with elevated privileges, usually as the root user.   | `sudo apt update`          |
| `chmod [perms] [file]` | Changes the read, write, and execute permissions of a file or directory. | `chmod +x script.sh`       |
| `chown [user] [file]`  | Changes the ownership of a file or directory.                            | `sudo chown root file.txt` |
| `useradd [user]`       | Creates a new user account.                                              | `sudo useradd rahim`       |
| `passwd [user]`        | Creates or changes a user's password.                                    | `sudo passwd rahim`        |

---

##  5. Networking Commands

| Command             | Definition / Purpose                                                                                                       | Example                             |
| :------------------ | :------------------------------------------------------------------------------------------------------------------------- | :---------------------------------- |
| `ping [host]`       | Tests network connectivity between your system and a host.                                                                 | `ping google.com`                   |
| `ip a`              | Displays IP addresses, network interfaces, and related network information.                                                | `ip a`                              |
| `ifconfig`          | Displays or configures network interfaces. It is largely replaced by the `ip` command on modern Linux systems.             | `ifconfig`                          |
| `curl [url]`        | Transfers or retrieves data from a URL. Commonly used for testing websites and APIs.                                       | `curl https://example.com`          |
| `wget [url]`        | Downloads files from the internet.                                                                                         | `wget https://example.com/file.zip` |
| `netstat -tuln`     | Displays listening TCP/UDP ports and network connections. `netstat` may need to be installed separately on modern systems. | `netstat -tuln`                     |
| `ssh [user]@[host]` | Connects securely to a remote system using SSH.                                                                            | `ssh user@192.168.1.1`              |

---

##  6. Package Management

> **Note:** Ubuntu and Debian-based distributions commonly use `apt`. Red Hat-based distributions commonly use `dnf` or, on older systems, `yum`.

| Command                  | Definition / Purpose                                     | Example                |
| :----------------------- | :------------------------------------------------------- | :--------------------- |
| `sudo apt update`        | Updates the local package repository information.        | `sudo apt update`      |
| `sudo apt upgrade`       | Upgrades installed packages to newer available versions. | `sudo apt upgrade`     |
| `sudo apt install [pkg]` | Installs a new software package.                         | `sudo apt install git` |
| `sudo apt remove [pkg]`  | Removes an installed software package.                   | `sudo apt remove git`  |

---

##  7. Miscellaneous Commands

| Command         | Definition / Purpose                                                          | Example             |
| :-------------- | :---------------------------------------------------------------------------- | :------------------ |
| `clear`         | Clears the terminal screen.                                                   | `clear`             |
| `history`       | Displays previously executed commands.                                        | `history`           |
| `alias`         | Creates a shortcut for a command or a group of commands.                      | `alias cls='clear'` |
| `man [command]` | **Manual:** Displays the official manual and usage information for a command. | `man ls`            |
| `exit`          | Exits the current terminal session or shell.                                  | `exit`              |

---

##  Quick Learning Tip

For cybersecurity and networking, focus especially on:

* File and directory management
* Linux permissions
* Users and groups
* Processes and system resources
* Networking commands
* SSH
* Package management
* Logs and `grep`
* Shell scripting
* `sudo` and root privileges

These commands form an important foundation for Linux administration, networking, cybersecurity, and penetration testing.

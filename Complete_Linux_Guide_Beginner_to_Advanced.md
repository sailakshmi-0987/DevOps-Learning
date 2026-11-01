# Complete Linux Guide: Beginner to Advanced

**Linux • System Administration • Operating Systems • DevOps**

Linux is a foundational skill for System Administration, Cloud
Computing, DevOps, Cybersecurity, Networking and Infrastructure
Engineering.

This guide covers the Linux syllabus from fundamentals through advanced
internals and production operations. The goal is not merely to memorize
commands, but to understand what happens inside Linux when commands
execute, how the operating system manages resources, and how to
troubleshoot real systems.

------------------------------------------------------------------------

# 1. Complete Linux Learning Roadmap

1.  **Linux Fundamentals & Architecture** --- operating systems, kernel,
    distributions, shell, boot process, users and permissions.
2.  **Linux File System & Directory Management** --- filesystem
    hierarchy, paths, files, directories, links, permissions and
    ownership.
3.  **Linux Commands & Text Processing** --- `grep`, `find`, `sort`,
    `awk`, `sed`, `cut`, pipes, redirection and command chaining.
4.  **Process Management & OS Internals** --- processes, threads, PID,
    PCB, signals, scheduling, priorities and memory.
5.  **Archiving, Compression & Storage** --- `tar`, `gzip`, `zip`,
    partitions, filesystems, mounting, `df`, `du` and LVM.
6.  **Linux Administration** --- users, groups, sudo, services, systemd,
    packages, logs and scheduling.
7.  **Networking & Security** --- IP, DNS, SSH, firewall, ports,
    routing, permissions and hardening.
8.  **Shell Scripting & Automation** --- Bash variables, loops,
    functions, conditions, automation and cron.
9.  **Advanced Linux Internals & Troubleshooting** --- kernel, system
    calls, virtual memory, namespaces, cgroups, performance and
    debugging.
10. **Production Linux & DevOps** --- servers, Docker, monitoring,
    backups, CI/CD and infrastructure management.

------------------------------------------------------------------------

# PART 2 --- Linux Fundamentals

## 2. What Is Linux?

Linux is an open-source, Unix-like operating system kernel.

An operating system acts as an intermediary between hardware and
applications. When you open a browser, for example:

1.  The application requests memory.
2.  The OS manages memory allocation.
3.  The CPU executes instructions.
4.  The kernel communicates with hardware through drivers.
5.  The application displays the webpage.

**Technically, Linux is the kernel.** A complete Linux operating system
distribution includes the kernel, system utilities, libraries, package
managers and other software.

## 3. Linux Architecture

The major layers are:

  Layer                   Responsibility
  ----------------------- ---------------------------------------------
  Hardware                CPU, RAM, disk, network devices
  Kernel                  Manages hardware and system resources
  System call interface   Allows programs to request kernel services
  System libraries        Provide reusable interfaces to system calls
  Shell                   Accepts and interprets user commands
  Applications            Browsers, editors, servers and utilities

### Linux Kernel

The kernel is the core component of Linux. Its major responsibilities
include:

1.  Process management
2.  Memory management
3.  Device management
4.  Filesystem management
5.  Networking
6.  Security and access control
7.  Resource allocation

Example:

``` bash
cat file.txt
```

The `cat` program requests the operating system to read the file. The
kernel handles the underlying file operations and returns the data.

### Kernel Space vs User Space

-   **User space:** Where normal applications and processes execute.
-   **Kernel space:** Where the kernel executes privileged operations.

Applications cannot directly access arbitrary hardware resources. They
request privileged services through system calls.

Common system calls:

  System call   Purpose
  ------------- --------------------------
  `open()`      Open a file
  `read()`      Read data
  `write()`     Write data
  `fork()`      Create a process
  `execve()`    Execute a program
  `wait()`      Wait for a child process
  `mmap()`      Map memory

Practical example:

``` bash
strace ls
```

This traces system calls made by `ls`, if `strace` is installed.

## 4. Linux Distributions

A Linux distribution packages the Linux kernel with utilities and
software required to operate a system.

  Distribution                      Typical use
  --------------------------------- ---------------------------------------------------
  Ubuntu                            Development, cloud and servers; beginner-friendly
  Red Hat Enterprise Linux (RHEL)   Enterprise infrastructure
  Debian                            Stable servers and desktops
  Fedora                            Modern Linux technologies and recent packages
  Arch Linux                        Highly customizable, rolling-release system

### Distribution Families and Package Managers

  Distribution family   Package manager   Package format
  --------------------- ----------------- ----------------
  Ubuntu / Debian       `apt`             `.deb`
  RHEL / Fedora         `dnf`             `.rpm`
  Arch                  `pacman`          `.pkg.tar`

Examples:

``` bash
# Ubuntu / Debian
sudo apt update
sudo apt install nginx

# RHEL / Fedora
sudo dnf install nginx

# Arch
sudo pacman -S nginx
```

## 5. Linux Shell and Command-Line Interface

A shell is a command interpreter that accepts user commands and executes
programs.

Popular shells:

  Shell    Description
  -------- --------------------------------------
  `sh`     Traditional Unix shell
  `bash`   Bourne Again Shell
  `zsh`    Interactive shell with customization
  `fish`   User-friendly interactive shell
  `ksh`    Korn shell

Check your shell:

``` bash
echo "$SHELL"
```

Check available shells:

``` bash
cat /etc/shells
```

Remember:

-   **Terminal:** The interface through which you interact with the
    shell.
-   **Shell:** The program interpreting commands.
-   **Kernel:** The core operating system.

## 6. Basic Linux Navigation Commands

  Command      Purpose
  ------------ ---------------------------------------
  `pwd`        Print current directory
  `ls`         List directory contents
  `cd`         Change directory
  `clear`      Clear terminal
  `whoami`     Display current username
  `hostname`   Display system hostname
  `date`       Display date and time
  `uname -a`   Display kernel and system information
  `history`    Display previously executed commands
  `man`        Open manual pages

Practice:

``` bash
pwd
ls
ls -l
ls -la
cd /etc
pwd
cd ..
pwd
```

Path symbols:

-   `/` --- root directory.
-   `~` --- current user's home directory.
-   `.` --- current directory.
-   `..` --- parent directory.

------------------------------------------------------------------------

# PART 3 --- Linux File System & Directory Management

## 7. Linux Filesystem Hierarchy

Linux follows a hierarchical filesystem structure beginning at `/`.

  Directory   Purpose
  ----------- ----------------------------------------------------
  `/`         Root of filesystem
  `/home`     Normal users' home directories
  `/root`     Root user's home directory
  `/etc`      System configuration files
  `/var`      Variable data, logs and caches
  `/tmp`      Temporary files
  `/usr`      User applications and shared data
  `/bin`      Essential user commands
  `/sbin`     System administration commands
  `/boot`     Bootloader and kernel-related files
  `/dev`      Device files
  `/proc`     Virtual filesystem with process/kernel information
  `/sys`      Kernel and device information
  `/mnt`      Temporary mount point
  `/media`    Removable media mount points
  `/opt`      Optional third-party software

Important distinctions:

-   `/proc` does not store ordinary files on disk. It exposes kernel and
    process information.
-   `/dev` contains device interfaces.
-   `/etc` stores many system configuration files.

## 8. Creating and Managing Files

### Create directories

``` bash
mkdir projects
mkdir -p projects/linux/day1
```

### Create files

``` bash
touch file.txt
```

### Copy files

``` bash
cp file.txt backup.txt
cp -r folder1 folder2
```

### Move and rename

``` bash
mv file.txt newfile.txt
mv newfile.txt /tmp/
```

### Delete

``` bash
rm file.txt
rmdir empty_folder
rm -r folder
```

**Warning:** `rm -rf` can permanently delete large directory trees.
Never experiment with it on system directories or important data.

## 9. Viewing File Contents

``` bash
cat file.txt
less file.txt
more file.txt
head file.txt
tail file.txt
```

Useful variations:

``` bash
head -n 5 file.txt
tail -n 10 file.txt
tail -f /var/log/syslog
```

`tail -f` is useful for monitoring logs in real time.

## 10. Absolute Paths vs Relative Paths

Absolute path:

``` text
/home/user/documents/file.txt
```

Relative path:

``` text
documents/file.txt
```

An absolute path starts at `/`. A relative path starts from the current
working directory.

## 11. Hidden Files

In Linux, filenames beginning with `.` are hidden by default.

``` bash
touch .env
mkdir .config
ls -la
```

Examples include `.bashrc`, `.profile`, `.ssh` and `.gitconfig`.

## 12. Linux File Types

Linux treats many resources as files.

Check file types:

``` bash
ls -l
file filename
```

  File type          Meaning                   Symbol
  ------------------ ------------------------- --------
  Regular file       Text, image, executable   `-`
  Directory          Directory                 `d`
  Symbolic link      Link to another path      `l`
  Character device   Character-based device    `c`
  Block device       Block storage device      `b`
  Named pipe         FIFO                      `p`
  Socket             IPC endpoint              `s`

## 13. Linux Permissions

Linux has three permission categories:

-   User (u)
-   Group (g)
-   Others (o)

Permission values:

-   Read (`r`) = 4
-   Write (`w`) = 2
-   Execute (`x`) = 1

Example:

``` text
-rwxr-xr--
```

  Owner   Group   Others
  ------- ------- --------
  `rwx`   `r-x`   `r--`
  7       5       4

Therefore:

``` bash
chmod 754 script.sh
```

Other commands:

``` bash
chmod u+x script.sh
chmod g-w file.txt
chown user file.txt
chown user:group file.txt
```

Advanced topics:

-   SUID
-   SGID
-   Sticky bit
-   ACLs
-   umask
-   Linux capabilities

------------------------------------------------------------------------

# PART 4 --- Linux Command Operations & Text Processing

## 14. Understanding Linux Command Syntax

General syntax:

``` text
command [options] [arguments]
```

Example:

``` bash
ls -l /home
```

-   `ls` --- command.
-   `-l` --- option.
-   `/home` --- argument.

Options can be short or long:

``` bash
ls -a
ls --all
```

## 15. Searching Files and Directories

``` bash
find /home -name "file.txt"
find . -type f
find . -type d
find . -name "*.log"
```

Search by size:

``` bash
find /var/log -size +10M
```

Search by modification time:

``` bash
find . -mtime -1
```

## 16. Searching Inside Files with grep

``` bash
grep "error" logfile.txt
grep -i "error" logfile.txt
grep -n "error" logfile.txt
grep -r "password" /etc
```

  Option   Meaning
  -------- ----------------------
  `-i`     Ignore case
  `-n`     Display line number
  `-r`     Recursive search
  `-v`     Invert match
  `-c`     Count matching lines
  `-w`     Match whole words

## 17. Text Processing Commands

  Command   Purpose
  --------- -------------------------------------
  `grep`    Search patterns
  `awk`     Process structured text and columns
  `sed`     Stream editing
  `cut`     Extract columns
  `sort`    Sort data
  `uniq`    Remove adjacent duplicate lines
  `wc`      Count lines, words and characters
  `tr`      Translate characters
  `tee`     Write output to file and terminal
  `xargs`   Build command arguments from input

Example file `students.txt`:

``` text
Sai 90
Ram 80
John 75
Lakshmi 95
```

Extract names:

``` bash
awk '{print $1}' students.txt
```

Extract marks:

``` bash
awk '{print $2}' students.txt
```

Find a name:

``` bash
grep "Sai" students.txt
```

Count lines:

``` bash
wc -l students.txt
```

Sort by marks:

``` bash
sort -k2 -n students.txt
```

Replace text using `sed`:

``` bash
sed 's/Linux/Ubuntu/g' file.txt
```

## 18. Input/Output Redirection

Linux has three standard streams:

  Stream     File descriptor Purpose
  -------- ----------------- ---------------
  stdin                    0 Input
  stdout                   1 Normal output
  stderr                   2 Error output

Examples:

``` bash
echo "Hello" > file.txt
echo "World" >> file.txt
cat < file.txt
ls /wrong 2> error.log
ls /wrong > output.log 2>&1
```

-   `>` overwrites a file.
-   `>>` appends to a file.
-   `2>` redirects errors.
-   `2>&1` redirects errors to the same destination as standard output.

## 19. Pipes

A pipe connects the output of one command to the input of another.

``` bash
ps aux | grep nginx
```

More examples:

``` bash
ls -l | wc -l
cat access.log | grep "404"
history | tail -10
```

------------------------------------------------------------------------

# PART 5 --- Linux Process Management & OS Internals

## 20. What Is a Process?

A process is an instance of a running program.

For example, `firefox` is a program. When you open Firefox, the
operating system creates one or more processes.

Important process concepts:

  Concept      Meaning
  ------------ ---------------------------------------
  PID          Process ID
  PPID         Parent Process ID
  UID          User ID
  GID          Group ID
  PCB          Process Control Block
  State        Current process state
  Priority     Scheduling priority
  Nice value   User-adjustable scheduling preference

## 21. Process Creation in Linux

A common process creation sequence:

1.  A parent process calls `fork()`.
2.  A child process is created.
3.  The child may call `exec()` to load another program.
4.  The parent may call `wait()` to collect the child's exit status.

C program:

``` c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        printf("Child PID: %d\n", getpid());
        printf("Parent PID: %d\n", getppid());
    }
    else if (pid > 0) {
        wait(NULL);
        printf("Parent PID: %d\n", getpid());
    }
    else {
        perror("fork");
    }

    return 0;
}
```

Compile and run:

``` bash
gcc process.c -o process
./process
```

## 22. Process States

  State   Meaning
  ------- -----------------------
  R       Running or runnable
  S       Interruptible sleep
  D       Uninterruptible sleep
  T       Stopped
  Z       Zombie

**Zombie process:** A child process has terminated, but its parent has
not yet collected its exit status.

**Orphan process:** A child continues after its parent terminates. It is
adopted by an appropriate system process, typically PID 1 or a
subreaper.

## 23. Viewing Processes

``` bash
ps
ps -ef
ps aux
top
htop
```

Inspect a particular process:

``` bash
ps -p 1234 -o pid,ppid,user,stat,ni,cmd
```

Process tree:

``` bash
pstree
```

## 24. Foreground and Background Processes

Foreground:

``` bash
sleep 100
```

The terminal waits for the command to finish.

Background:

``` bash
sleep 100 &
```

The shell returns control immediately.

Job management:

``` bash
jobs
fg
bg
```

Suspend a foreground process with `Ctrl+Z`. Interrupt a foreground
process with `Ctrl+C`.

## 25. Process Termination and Signals

Signals allow processes to receive notifications and control requests.

  Signal      Number Purpose
  --------- -------- ---------------------
  SIGINT           2 Interrupt
  SIGKILL          9 Force termination
  SIGTERM         15 Request termination
  SIGSTOP         19 Stop process
  SIGCONT         18 Continue process
  SIGHUP           1 Hangup

Commands:

``` bash
kill -15 PID
kill -9 PID
kill -l
pkill nginx
```

Prefer SIGTERM first. SIGKILL should be a last resort because it does
not allow the process to clean up.

## 26. Process Priorities and Nice Values

Nice values range from -20 to +19:

-   -20 = Higher scheduling preference.
-   +19 = Lower scheduling preference.
-   0 = Default nice value.

``` bash
nice -n 10 command
renice 5 -p 1234
ps -eo pid,ni,pri,comm
```

## 27. Linux Services and System Control

Linux systems commonly use `systemd` to manage services.

Examples include SSH, Nginx, Docker and cron.

``` bash
systemctl status ssh
systemctl start ssh
systemctl stop ssh
systemctl restart ssh
systemctl enable ssh
systemctl disable ssh
```

-   `start` --- Starts now.
-   `enable` --- Configures automatic startup during boot.
-   `restart` --- Stops and starts again.
-   `status` --- Displays service state.

## 28. Shutdown and Restart

``` bash
sudo shutdown -h now
sudo shutdown -r now
sudo reboot
sudo poweroff
```

These commands affect the entire system. On an office machine, VM or
shared server, use them only when authorized.

------------------------------------------------------------------------

# PART 6 --- Linux Archiving, Compression & Storage

## 29. Archiving vs Compression

-   **Archiving:** Combining multiple files into a single archive.
-   **Compression:** Reducing the amount of storage required.

`tar` combines files. `gzip` compresses files. `tar.gz` combines and
compresses.

## 30. Working with TAR

Create an archive:

``` bash
tar -cvf backup.tar folder/
```

Extract:

``` bash
tar -xvf backup.tar
```

List contents:

``` bash
tar -tvf backup.tar
```

Create a compressed archive:

``` bash
tar -czvf backup.tar.gz folder/
```

Extract a compressed archive:

``` bash
tar -xzvf backup.tar.gz
```

  Option   Meaning
  -------- ------------------
  `c`      Create
  `x`      Extract
  `v`      Verbose
  `f`      Archive filename
  `t`      List contents
  `z`      gzip
  `j`      bzip2
  `J`      xz

## 31. ZIP Operations

``` bash
zip archive.zip file1.txt file2.txt
zip -r archive.zip folder/
unzip archive.zip
unzip -l archive.zip
```

## 32. Compression Formats

  Format   Tool    Characteristics
  -------- ------- --------------------------------------------
  `.gz`    gzip    Fast general-purpose compression
  `.bz2`   bzip2   Often higher compression, slower
  `.xz`    xz      Often high compression, more CPU-intensive
  `.zip`   zip     Convenient cross-platform archive
  `.tar`   tar     Archive, not necessarily compressed

## 33. Linux Filesystems

A filesystem determines how files are organized, stored, retrieved and
managed on a storage device.

  Filesystem   Characteristics
  ------------ ---------------------------------------------------------
  ext4         General-purpose Linux filesystem
  XFS          High-performance filesystem, common in enterprise Linux
  Btrfs        Copy-on-write, snapshots and checksumming
  FAT32        Common removable-media compatibility
  NTFS         Common Windows filesystem

## 34. Inodes

An inode stores metadata about a file, including:

-   File permissions
-   Owner and group
-   File size
-   Timestamps
-   Pointers/references to data blocks

An inode does not normally store the filename. Directory entries map
filenames to inode numbers.

Check inode:

``` bash
ls -i file.txt
stat file.txt
```

Check inode usage:

``` bash
df -i
```

## 35. Disk Space Monitoring

``` bash
df -h
df -Th
du -sh folder/
du -ah
lsblk
blkid
```

-   `df` --- Filesystem-level available and used space.
-   `du` --- Disk space used by files/directories.
-   `lsblk` --- Block devices and their relationships.
-   `blkid` --- Filesystem identification and UUID information.

## 36. Mounting and Unmounting

Mounting makes a filesystem accessible at a directory called a mount
point.

``` bash
sudo mkdir /mnt/data
sudo mount /dev/sdb1 /mnt/data
```

Check mounts:

``` bash
findmnt
mount
df -h
```

Unmount:

``` bash
sudo umount /mnt/data
```

Advanced storage topics:

-   Disk partitions
-   MBR vs GPT
-   Swap partitions and swap files
-   LVM (Logical Volume Manager)
-   RAID
-   `/etc/fstab`
-   UUIDs
-   Filesystem repair
-   Disk quotas

**Safety:** Do not experiment with formatting, partitioning or mounting
unknown disks on an office laptop.

------------------------------------------------------------------------

# PART 7 --- Linux System Administration

## 37. Linux Users and Groups

Linux is a multi-user operating system. Every process executes with an
associated user identity and group credentials.

Important files:

  File             Purpose
  ---------------- ------------------------------------
  `/etc/passwd`    User account information
  `/etc/shadow`    Password hashes and password aging
  `/etc/group`     Group information
  `/etc/gshadow`   Secure group information

Commands:

``` bash
whoami
id
who
w
users
```

Create a user:

``` bash
sudo useradd -m sai
sudo passwd sai
```

Create a group:

``` bash
sudo groupadd developers
```

Add user to group:

``` bash
sudo usermod -aG developers sai
```

Switch user:

``` bash
su - sai
```

## 38. Root User vs sudo

Root is the superuser with UID 0.

`sudo` allows authorized users to execute commands with elevated
privileges.

``` bash
sudo apt update
sudo -l
```

Never use root privileges unnecessarily.

## 39. Package Management

Ubuntu:

``` bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
```

RHEL:

``` bash
sudo dnf check-update
sudo dnf upgrade
sudo dnf install nginx
sudo dnf remove nginx
```

## 40. Linux Boot Process

Typical boot sequence:

1.  BIOS/UEFI initializes hardware.
2.  Bootloader is loaded.
3.  GRUB loads the Linux kernel and initramfs.
4.  Kernel initializes hardware and memory management.
5.  Kernel starts the initial userspace process.
6.  Systemd initializes services and targets.
7.  Login screen or terminal becomes available.

Check boot information:

``` bash
uname -r
systemd-analyze
systemd-analyze blame
journalctl -b
```

Important concepts:

-   BIOS vs UEFI
-   MBR vs GPT
-   GRUB
-   Initramfs
-   Kernel initialization
-   PID 1
-   Systemd targets
-   Recovery mode

## 41. Linux Logging

Logs help administrators investigate system events and failures.

  -----------------------------------------------------------------------
  Log                                 Purpose
  ----------------------------------- -----------------------------------
  `/var/log/syslog`                   General system messages on many
                                      Debian-based systems

  `/var/log/auth.log`                 Authentication logs on many
                                      Debian-based systems

  `/var/log/messages`                 General system messages on many
                                      RHEL-based systems

  `/var/log/secure`                   Authentication logs on many
                                      RHEL-based systems

  `/var/log/kern.log`                 Kernel logs on systems that
                                      maintain this file
  -----------------------------------------------------------------------

Commands:

``` bash
journalctl
journalctl -b
journalctl -u ssh
journalctl -p err
dmesg
```

Example: If SSH is not working, investigate:

``` bash
systemctl status ssh
journalctl -u ssh
ss -tulnp
```

## 42. Scheduled Jobs

`cron` executes commands on a recurring schedule.

``` bash
crontab -e
crontab -l
```

Cron format:

``` text
* * * * * command
| | | | |
| | | | +--- Day of week
| | | +----- Month
| | +------- Day of month
| +--------- Hour
+----------- Minute
```

Example:

``` bash
0 2 * * * /home/sai/backup.sh
```

This runs the script daily at 2 AM.

Also learn:

-   `at`
-   systemd timers
-   cron environment variables
-   job output and logging

------------------------------------------------------------------------

# PART 8 --- Linux Networking

## 43. Basic Networking Commands

  Command        Purpose
  -------------- ----------------------------
  `ip addr`      Display IP addresses
  `ip link`      Display network interfaces
  `ip route`     Display routing table
  `ping`         Test connectivity
  `ss`           Display socket information
  `curl`         Make HTTP requests
  `wget`         Download files
  `traceroute`   Trace network path
  `dig`          DNS lookup
  `nslookup`     DNS lookup
  `hostname`     Display hostname

Examples:

``` bash
ip addr
ip route
ping google.com
ss -tulnp
curl https://example.com
```

## 44. Important Networking Concepts

Understand:

1.  IP addresses
2.  MAC addresses
3.  Subnet masks
4.  Default gateways
5.  DNS
6.  DHCP
7.  TCP vs UDP
8.  Ports and sockets
9.  Routing
10. Firewalls
11. HTTP and HTTPS
12. SSH

Common ports:

     Port Protocol/service
  ------- ------------------------------
    20/21 FTP
       22 SSH
       23 Telnet
       25 SMTP
       53 DNS
    67/68 DHCP
       80 HTTP
      110 POP3
      143 IMAP
      443 HTTPS
     3306 MySQL
     5432 PostgreSQL
     6379 Redis
     8080 Common alternative HTTP port

## 45. SSH --- Secure Shell

SSH allows secure remote access to another machine.

Connect:

``` bash
ssh username@server_ip
```

Generate keys:

``` bash
ssh-keygen -t ed25519
```

Copy public key:

``` bash
ssh-copy-id username@server_ip
```

Copy files:

``` bash
scp file.txt username@server_ip:/home/username/
```

Understand:

-   SSH client vs SSH server
-   Public key vs private key
-   Password authentication
-   Key-based authentication
-   SSH configuration
-   SSH agent
-   Port forwarding

## 46. Linux Firewall

A firewall controls incoming and outgoing network traffic.

On Ubuntu, you may encounter UFW:

``` bash
sudo ufw status
sudo ufw allow 22
sudo ufw allow 80
sudo ufw enable
```

Other tools:

-   iptables
-   nftables
-   firewalld

Do not enable or change firewall rules on an office machine without
authorization.

------------------------------------------------------------------------

# PART 9 --- Shell Scripting & Automation

## 47. What Is Shell Scripting?

A shell script is a file containing commands that are executed by a
shell.

Example:

``` bash
#!/bin/bash

echo "Welcome to Linux"
date
whoami
pwd
```

Save as `welcome.sh` and execute:

``` bash
chmod +x welcome.sh
./welcome.sh
```

## 48. Variables

``` bash
#!/bin/bash

name="Sai"
age=22

echo "Name: $name"
echo "Age: $age"
```

There should be no spaces around `=` when assigning shell variables.

## 49. Taking User Input

``` bash
#!/bin/bash

echo "Enter your name:"
read name

echo "Welcome $name"
```

## 50. Conditional Statements

``` bash
#!/bin/bash

read -p "Enter a number: " num

if [ "$num" -gt 10 ]; then
    echo "Greater than 10"
else
    echo "10 or less"
fi
```

  Operator   Meaning
  ---------- -----------------------
  `-eq`      Equal
  `-ne`      Not equal
  `-gt`      Greater than
  `-lt`      Less than
  `-ge`      Greater than or equal
  `-le`      Less than or equal

## 51. Loops

For loop:

``` bash
for i in {1..5}
do
    echo "$i"
done
```

While loop:

``` bash
i=1

while [ "$i" -le 5 ]
do
    echo "$i"
    ((i++))
done
```

## 52. Functions

``` bash
#!/bin/bash

greet() {
    echo "Hello $1"
}

greet "Linux"
```

## 53. Advanced Shell Scripting

Learn:

-   Positional parameters: `$1`, `$2`, `$@`, `$#`
-   Exit status: `$?`
-   Process ID: `$$`
-   Command substitution
-   Arrays
-   Case statements
-   Functions and return codes
-   `set -euo pipefail`
-   Error handling
-   Logging
-   Signals and traps
-   Regular expressions
-   Input validation

## 54. Practical Automation Projects

1.  Automated backup script.
2.  Disk usage monitoring script.
3.  CPU and memory monitoring script.
4.  Log file analyzer.
5.  User creation automation.
6.  Service health-check script.
7.  Automated old-log cleanup.
8.  Server status report generator.

------------------------------------------------------------------------

# PART 10 --- Advanced Linux Internals

## 55. Memory Management

Understand:

-   Physical memory
-   Virtual memory
-   Virtual address space
-   Paging
-   Page tables
-   TLB
-   Page faults
-   Demand paging
-   Swapping
-   Memory fragmentation
-   Memory allocation

Check memory:

``` bash
free -h
cat /proc/meminfo
vmstat 1
```

Check process memory:

``` bash
ps aux
top
```

## 56. CPU Management

Understand:

-   CPU scheduling
-   Process scheduling
-   Context switching
-   Multitasking
-   Multithreading
-   CPU affinity
-   Load average
-   Scheduler priorities

Commands:

``` bash
lscpu
top
uptime
mpstat
```

## 57. Inter-Process Communication (IPC)

Processes need mechanisms to communicate with each other.

  Mechanism            Purpose
  -------------------- ------------------------------------------------------------
  Pipes                Communication between related processes
  Named pipes (FIFO)   Communication through a filesystem entry
  Message queues       Exchange structured messages
  Shared memory        Share memory between processes
  Semaphores           Synchronization
  Signals              Notify processes of events
  Sockets              Communication between processes, locally or over a network

Inspect IPC resources:

``` bash
ipcs
ipcs -m
ipcs -q
ipcs -s
```

## 58. Linux Kernel Modules

A kernel module is code that can be loaded into or removed from the
running kernel. Examples include device drivers.

``` bash
lsmod
modinfo module_name
sudo modprobe module_name
sudo modprobe -r module_name
```

Important concepts:

-   Monolithic kernel
-   Loadable kernel modules
-   Device drivers
-   Kernel version
-   Kernel logs
-   Kernel configuration

## 59. Linux Namespaces and Cgroups

These are fundamental to container technology.

**Namespaces** isolate resources such as:

-   Process IDs
-   Network interfaces
-   Mount points
-   Hostnames
-   Users
-   IPC resources

**Control groups (cgroups)** control and account for resource usage such
as:

-   CPU
-   Memory
-   I/O
-   Process limits

Commands:

``` bash
lsns
cat /proc/self/cgroup
```

## 60. Advanced Linux Troubleshooting

  Problem                 Useful commands
  ----------------------- --------------------------------
  High CPU                `top`, `ps`, `mpstat`
  High memory usage       `free`, `ps`, `vmstat`
  Disk full               `df`, `du`, `find`
  Service failure         `systemctl`, `journalctl`
  Network failure         `ip`, `ping`, `ss`, `dig`
  Slow system             `uptime`, `vmstat`, `iostat`
  File permission issue   `ls -l`, `stat`, `id`, `namei`
  Process stuck           `ps`, `strace`, `lsof`
  Boot failure            `journalctl -b`, `systemctl`

Additional advanced tools:

``` bash
strace
ltrace
lsof
fuser
iostat
sar
perf
tcpdump
```

------------------------------------------------------------------------

# PART 11 --- Linux in Production & DevOps

## 61. Linux Server Administration

Learn:

-   Remote server administration
-   SSH hardening
-   User and group administration
-   Service management
-   Log rotation
-   Disk monitoring
-   Backup and recovery
-   Software installation
-   Security updates
-   Resource monitoring
-   Incident troubleshooting

## 62. Linux and Docker

Docker relies heavily on Linux kernel features.

  Linux concept   Docker usage
  --------------- --------------------------------
  Namespaces      Process and resource isolation
  Cgroups         Resource limits
  Filesystems     Container storage layers
  Networking      Container networking
  Capabilities    Fine-grained privileges
  OverlayFS       Container image layers

Commands to learn:

``` bash
docker ps
docker images
docker run
docker exec
docker logs
docker inspect
docker stop
```

## 63. Linux and Kubernetes

Kubernetes workloads often run as containers on Linux-based nodes.

Learn:

-   Container runtime
-   Kubelet
-   Pod lifecycle
-   Container networking
-   Persistent volumes
-   Node resource management
-   Linux namespaces
-   Cgroups
-   Container security

## 64. Linux and Cloud Computing

Linux is widely used on cloud servers.

Learn how to:

1.  Create a Linux EC2 instance.
2.  Connect using SSH.
3.  Install web servers.
4.  Configure security groups.
5.  Configure firewall rules.
6.  Deploy applications.
7.  Monitor system resources.
8.  Configure backups.
9.  Troubleshoot connectivity.

------------------------------------------------------------------------

# PART 12 --- Practical Linux Laboratory

## 65. Recommended Practice Environments

Use three environments:

### 1. WSL Ubuntu

Use it for everyday commands, shell scripting, permissions, processes
and networking exercises.

### 2. VirtualBox

Use a separate Linux VM for booting, users, services, disks, partitions
and system administration experiments.

### 3. Cloud Linux Server

Later, use a personal cloud VM to practise remote administration,
deployment, monitoring and production troubleshooting.

## 66. 30-Day Linux Practical Roadmap

Suggested schedule: 1.5--2 hours daily, with more time for hands-on
exercises.

  -----------------------------------------------------------------------
  Days                    Topics                  Practical outcome
  ----------------------- ----------------------- -----------------------
  1--3                    Fundamentals,           Understand Linux
                          architecture, kernel,   architecture
                          shell                   

  4--6                    Navigation, hierarchy,  Work confidently with
                          file management         files

  7--9                    Permissions, users,     Manage access
                          groups                  

  10--12                  grep, find, awk, sed,   Process real text data
                          pipes                   

  13--15                  Processes, PID,         Manage processes
                          signals, priorities     

  16--18                  Services, boot, logs,   Administer services
                          systemd                 

  19--21                  tar, compression,       Manage storage
                          storage, filesystems    

  22--23                  Networking, SSH, ports  Troubleshoot
                                                  connectivity

  24--26                  Bash scripting and cron Automate tasks

  27--28                  Memory, CPU, IPC,       Understand internals
                          kernel                  

  29--30                  Troubleshooting and     Practice production
                          projects                scenarios
  -----------------------------------------------------------------------

## 67. Ten Hands-on Linux Projects

### Project 1 --- Linux File Manager (Beginner)

Create a directory structure, manage files, copy, move, rename and
delete files.

Skills: `mkdir`, `touch`, `cp`, `mv`, `rm`, `find`.

### Project 2 --- User & Permission Manager (Beginner)

Create multiple users, groups and shared directories with appropriate
permissions.

Skills: `useradd`, `groupadd`, `chmod`, `chown`, `umask`.

### Project 3 --- Log Analyzer (Intermediate)

Analyze a sample log file and find errors, warnings, IP addresses and
frequency counts.

Skills: `grep`, `awk`, `sed`, `sort`, `uniq`.

### Project 4 --- Process Monitor (Intermediate)

Monitor running processes, CPU consumption and memory usage.

Skills: `ps`, `top`, `kill`, `nice`, `free`.

### Project 5 --- Automated Backup (Intermediate)

Write a Bash script to back up directories and compress them.

Skills: Bash, `tar`, `gzip`, cron.

### Project 6 --- Service Management (Intermediate)

Install Nginx, manage its service and inspect logs.

Skills: `systemctl`, `journalctl`, package management.

### Project 7 --- Linux Network Troubleshooter (Advanced)

Investigate DNS resolution, port connectivity, routes and listening
services.

Skills: `ip`, `ss`, `ping`, `curl`, `dig`.

### Project 8 --- Disk Usage Monitor (Advanced)

Build an automated script that reports disk usage and warns when a
threshold is exceeded.

Skills: `df`, `du`, Bash, cron.

### Project 9 --- Linux Server Hardening (Advanced)

Configure SSH authentication, user access and firewall rules in a
disposable VM.

Skills: SSH, permissions, UFW, security.

### Project 10 --- Production Linux Server (Industry Level)

Deploy a web application on a Linux VM, configure Nginx, manage
services, monitor logs and automate backups.

Skills: Linux, Bash, Networking, Nginx, Docker, monitoring.

------------------------------------------------------------------------

# PART 13 --- Essential Linux Command Cheat Sheet

  Category             Commands
  -------------------- -------------------------------------
  Navigation           `pwd`, `ls`, `cd`
  Files                `touch`, `cat`, `cp`, `mv`, `rm`
  Directories          `mkdir`, `rmdir`, `find`
  Permissions          `chmod`, `chown`, `umask`
  Users                `whoami`, `id`, `useradd`, `passwd`
  Processes            `ps`, `top`, `kill`, `pgrep`
  Services             `systemctl`, `journalctl`
  Storage              `df`, `du`, `lsblk`, `mount`
  Archive              `tar`, `gzip`, `zip`, `unzip`
  Text processing      `grep`, `awk`, `sed`, `cut`
  Networking           `ip`, `ping`, `ss`, `curl`, `dig`
  System information   `uname`, `lscpu`, `free`, `uptime`
  Scheduling           `cron`, `crontab`, `at`
  Debugging            `strace`, `lsof`, `dmesg`

------------------------------------------------------------------------

# PART 14 --- Recommended Learning Resources

1.  **Linux Journey** --- Interactive Linux learning:
    https://linuxjourney.com/
2.  **The Linux Documentation Project** --- Linux documentation:
    https://tldp.org/
3.  **Ubuntu Documentation** --- Official Ubuntu guides:
    https://documentation.ubuntu.com/
4.  **Linux man-pages** --- Linux command and system-call documentation:
    https://man7.org/linux/man-pages/
5.  **The Linux Command Line** --- Free book and exercises:
    https://linuxcommand.org/tlcl.php

Use manual pages to learn commands:

``` bash
man ls
man grep
man chmod
man fork
```

You can also use:

``` bash
command --help
```

------------------------------------------------------------------------

# PART 15 --- Linux Knowledge Assessment

Try answering these questions after studying the relevant modules.

### 1. Which component manages CPU, memory and hardware?

A. Shell\
B. Kernel\
C. Terminal\
D. Compiler

**Answer: B --- Kernel.** The kernel manages hardware resources and core
operating system functions.

### 2. What happens when you execute `chmod 754 file.txt`?

A. Everyone gets full permissions\
B. Owner gets rwx, group gets r-x, others get r--\
C. Owner gets read only\
D. File becomes executable for everyone

**Answer: B.** 7 = rwx, 5 = r-x and 4 = r--.

### 3. Which command displays inode numbers?

A. `ls -l`\
B. `ls -i`\
C. `df -h`\
D. `statfs`

**Answer: B --- `ls -i`.** It displays the inode number associated with
each directory entry.

### 4. Which system call creates a child process?

A. `exec()`\
B. `read()`\
C. `fork()`\
D. `write()`

**Answer: C --- `fork()`.** It creates a child process by duplicating
the calling process.

### 5. Which command monitors a service's logs?

A. `journalctl -u service`\
B. `chmod service`\
C. `df service`\
D. `mkdir service`

**Answer: A --- `journalctl -u service`.** It filters journal entries
for a particular systemd unit.

### 6. Which Linux kernel feature helps isolate container processes?

A. Namespaces\
B. Cron\
C. GRUB\
D. Gzip

**Answer: A --- Namespaces.** They isolate process IDs, networks, mount
points and other resources.

------------------------------------------------------------------------

# PART 16 --- How to Practise Effectively

Do not try to learn all these topics in one sitting. Follow this
sequence:

1.  Understand the concept.
2.  Learn the commands.
3.  Execute each command yourself.
4.  Observe the output.
5.  Understand what happens internally.
6.  Solve a real-world problem using that concept.

A particularly important distinction:

**Linux command knowledge and Linux system knowledge are different.**

For example, knowing `ps` is useful, but understanding how Linux
creates, schedules and terminates processes is much more valuable.

## Suggested Study Method

For each topic, maintain four sections in your notes:

-   **Concept:** What is it and why is it needed?
-   **Commands:** Syntax, options and examples.
-   **Practical:** Execute commands and record outputs.
-   **Interview:** Explain the concept and answer scenario-based
    questions.

The best approach is to study Linux module by module, starting with
Linux Architecture, Kernel, System Calls, Shell and Boot Process, then
progressing to file management, process management, administration,
networking, scripting and advanced internals.

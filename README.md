# Linux Basics

Linux questions from: https://github.com/chassing/linux-sysadmin-interview-questions#general.

- HTTP Proxy: HTTP Proxy works as a middle man to filter content. Proxy sends and receives request on behalf of browser and filter content based on the ruleset.
- HTTPS: Extension of HTTP. Encrypted by Transport Layer Security (TLS). Ensures privacy and integrity of the exchanged data.
- SMTP: Standard for email transmission. Usually used by clients to send.
- IMAP/POP3: Used by clients to retrieve emails. POP3 is older.
- Parity: Extra bit to ensure integrity of string. Can only detect. Cannot correct.
- RAID:

| RAID level | Striping          | Mirroring | Parity                   |
| ---------- | ----------------- | --------- | ------------------------ |
| 0          | Yes               | No        | No                       |
| 1          | No                | Yes       | No                       |
| 2          | Yes (bit-level)   |           | Yes (Hamming-code)       |
| 3          | Yes (byte-level)  |           | Yes (dedicated)          |
| 4          | Yes (block-level) |           |                          |
| 5          | Yes (block-level) | Yes       | Yes (distributed)        |
| 6          | Yes (block-level) | Yes       | Yes (double-distributed) |

- More RAID:
	- RAID 10: Creates striped set from series of mirrored drives
	- RAID 01: Creates two stripes and mirrors them. Basically reads from two sets at once.
- Level 0 backup: First full backup.
- Incremental backup: Incremental backup is the backup of changed data from the last time. Level n backup will back up everything that has changed since n-1 backup.
- Filesystem hierarchy standard: Defines directory structure in Linux distributions.
	- /: Root directory. Everything appears under root directory.
	- /bin: Command binaries.
	- /boot: Boot loader files like kernel
	- /dev: device files
	- /etc: Anything that does not belong elsewhere. Not binries
	- /home: user home directories
	- /lib: libraries essential for binaries in /bin and /sbin
	- /media: mount points for removable media.
	- /mnt: Temporarily mounted filesystems.
	- /root: Home directory for the root user.
	- /opt: Optional software packages
	- /proc: Virtual filesystem providing process and kernel information as files.
	- /sbin: Essential system binaries.
	- /tmp: Temporary files.
	- /usr: Read-only user data.
		- /usr/bin: Non-essential command binaries for all users.
		- /usr/include: Standard include files
		- /usr/local/: Local data specific to host.
	- /var: variable files that changes during normal operation of the system.
		- /var/log: Stores log files.
		- /var/mail: Mailbox files
		- /var/cache: Application data
		- /var/tmp: Temporary files to be preserved between reboots.
- Linux UIDs:
  - Name of the administrator: root, admin, supervisor
  - UID of the supervisor: 0
  - UID 1 through 99 is reserved for special users like wheel, news, mail
- List all files along with hidden files: `ls -la`
- Remove all files in a directory: `rm -rf`
- Command for showing free/used memory: `free`
- Free memory in linux: Linux borrows unused memory for disk caching. OS will free memory if needed.
- Search for a string in a directory recursively: `grep -rnw 'string'`.
- `ifconfig` is replaced by `ip`.
- `df`: Shows disk space use of file system
- `du`: Estimate space usage of files.

| Number | Binary |
| ------ | ------ |
| 0      | 000    |
| 1      | 001    |
| 2      | 010    |
| 3      | 011    |
| 4      | 100    |
| 5      | 101    |
| 6      | 110    |
| 7      | 111    |

- `useradd <username>`: Add new user without login.
- `groupadd <groupname>`: Add new group
- `usermod -a -G groupname username`: Add user to group. `-a`: append, `-G`: to group.
- Delete user from group:
	- `gpasswd -d user group`
	- In debian: `deluser user group`
	- Edit `/etc/group`.
- Bash alias: Short abbreviation for long commands
- Change mail address of root/user: edit `etc/aliases` and then run `newaliases`.
- CTRL+z: sends `SIGSTOP` to the process. `SIGSTOP` pauses the process in it’s current step. To continue, `SIGCONT` needs to be sent.
- CTRL+c: sends `SIGINT` to the process. `SIGINT` terminates the process. The process can choose to ignore it.
- `etc/services`: This file is a local database. It specifies well-known port number for the services.
- `STDOUT`: Standard stream for output.
- `STDERR`: Standard stream for error.
- Redirect `STDOUT` and `STDERR` of a command: `cmd > /to/file 2>&1`. The `2>%1` part redirects `STDERR` to the same as the earlier one. Replacing `/to/file` to `/dev/null` will redirect everything to nothingness.
- `/dev/null`: Is a device implemented in software in unix systems. It is empty if read from it. Writing to it simply disappears.
- Difference between Unix and LInux:
	- Linux is open source, Unix is propietary.
	- Unix if from AT&T whereas the Linux is from Open Source Foundation.
	- Unix primarily uses CLI with a smaller support of hardwares available out there.
	- Linux supports much larger spectrum of hardwares.
	- Unix supports limited file system. Linux supports much larger spectrum of file systems.
- Telnet vs SSH
	- They both are network protocol for remotely accessing and managing a device.
	- Telnet sends all data (username and password included) in clear text.
	- SSH uses encryption for transmitting data.
	- Telnet uses TCP port 23 and SSH uses TCP port 22.
- Three load averages: 
	- Load averages for 1, 5 and 15 minues.
	- What the number means? Nice explanation here: http://blog.scoutapp.com/articles/2009/07/31/understanding-load-averages
	- The load average interpretation is dependent on number of cores available to the OS.
	- To know about info on each processor, `cat /proc/cpuinfo`.
- Linux Kernel Module (LKM): Pieces of code that can be loaded and unloaded into the kernel upon demand.
- Booting into Single-User Mode
	- CentOS: Athe GRUB splash screen at boot time, press any key to enter interactive menu. Select kernel version and then type `a` to append. Go to the end of the file and type `single`. Press `Enter` to exit edit mode.
- Linux runlevel: Run leve is a stat of `init` and it defines which system services will operate.
	- 0 Halt: Shuts down system.
	- 1 Single-User Mode: Local file systems are mounted, but network is not activated. Only allows root logins.
	- 2 Multi-User Mode: Same as 1. Allows non-root logins.
	- 3 Multi-User Mode with Networking: Stats the system normally
	- …
	- 6 Reboot: Reboots the system.
- Linux commands,
	- `awk`: Good for parsing preformatted data. For example `awk '/^UUID/ {print $1}' /etc/fstab` finds lines that starts with `UUID` from file `/etc/fstab` then prints the first column.
	- `tr`: `tr` is used to replace or remove specific characters from input data set. For example, `tr 'abcd' 'jkmn'` replaces all characters `abcd` to `jkmn`.
	- `cut`: Removes sections from each line of files.
	- …
- Bash command backgrounding:
	- `&` after a command in bash runs the command in the background. The shell does not wait for the command to finish and the return status is 0.
	- `& disown` removes the process from shell’s job control. But it still leaves it connected to the terminal. Shell won’t send it `SIGHUP`.
	- `nohup` disconnects the process form the terminal, redirects the output to `nohup.out` and shields it from `SIGHUP`.
- Linux packet filter: A software which checks header of packets as they pass through and decides. to `DROP` or `ACCEPT` the packet.
- Virtual memory: Using of a disk as an extension of RAM.
- Swap: Linux divides physical ram into parts called pages. Through swapping, pages can be stored to part of the hard disk called swap space.
- DNS:
	- NS: Specifies the authoritative nameservers for domain
	- A (address) record: Used to point domain to IP.
	- CNAME: Aliasing one name to another.
	- MX: Specified the domain to which mail is delivered.
- Sticky bit: STicky bit the restricted deletion bit. If set, users can only delete files and directories within if they are the owners.
- Immutable bit: If set, even `root` cannot delete the file. `chattr +i file` 
- `inode`: In Linux, each file or directory has an associated `inode`.
	- Can be seen by doing `ls -il`.
	- Contains metadata of the file and directory.
	- Size of the file in bytes.
	- Device ID of the file.
	- User ID and group ID of the file.
	- Information about the owner, group and world information about the file.
	- etc. etc.
- Hardlink and softlink
	- Hardlink points to the `inode` of the file. Renaming or changing the file does not effect the data.
	- Softlink points to the name of the file. Renaming the file will make the softlink invalid.
	- Softlinks can span file systems as. Hard links are valid within the file system.
- SSH Port forwarding: creates connection between a local computer and a remote machine.
	- Local vs Remote SSH forwarding: …
- Filesystem full but has space:
	- May be out of nodes. Check using `df -i`.
	- A process has opened a large file which since been deleted. The process needs to be killed.
- Deleting does not free space:
	- Even though deleted, some other process might be holding the file open. Restart or kill the process which is holding it. Can be used `lsof +L1` to find out which process is using a deleted or unlinked file.
- `ps` command: process status
	- Works by reading the files in the `/proc` filesystem.
- A child process dies and has no parent process to wait for it: called zombie process. It’s a problem because linux has finite number of process IDs. It can run out of process IDs.
- process states:
	- R: Running
	- S: interruptible sleep
	- T: Stopped
	- W: paging
- Process and threads:
	- Processes are running instance of a program.
	- Threads are flow of execution of the process.
- `exec` and `fork`:
	- `fork` makes a duplicate of the current process. The child process gets a different PID.
	- `exec` replaces the the entire process with a new program.
- `ping` and `tracertoute`
	- Utility for server packet response.
	- `traceroute` sends packes with increasing TTL.
- TCP vs UDP
	- Both are protocols used for sending bits of data.
	- TCP: Transmission Control Protocol
	- UDP: User Datagram Protocol
	- For UDP, packets are sent and the sender will not wait for the recipients confirmation.
- Networking:
  - Cat 5: 
    - Two copper cable twisted
    - Max freq 100MHz
  - Cat 6:
    - Four cable twisted
    - Max freq 250MHz
    - Less crosstalk
  - Cat 6a:
    - 50MHz
  - Crosstalk:
    - Electromagnetic interference from one unshielded twisted pair to another.



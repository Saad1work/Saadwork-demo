# Linux Short Notes --- DevOps

## 1. History of Linux

-   Linux is a free and open-source operating system related to the Unix
    family.
-   Linus Torvalds developed Linux in 1991.
-   The first Linux code (0.01) was posted to the Minix newsgroup on 17
    September 1991.
-   Version 0.02 was released on 5 October 1991.
-   The notes state that Linux is widely used on supercomputers.

## 2. Linux File System Hierarchy

Linux organizes files and directories in a single-rooted, tree-like
structure. The root directory is `/`.

  -----------------------------------------------------------------------
  Path                                Purpose
  ----------------------------------- -----------------------------------
  `/`                                 Root; starting point of the
                                      filesystem

  `/root`                             Home directory of the root
                                      (superuser)

  `/bin`                              Common user command binaries

  `/sbin`                             System-administration binaries

  `/dev`                              Device files, such as terminal and
                                      USB device entries

  `/var`                              Variable data, including logs and
                                      data that can grow

  `/var/log`                          System and application logs

  `/var/lib`                          Application/package state data

  `/var/mail`                         Mail storage

  `/var/tmp`                          Temporary files intended to persist
                                      longer than `/tmp` on some systems

  `/mnt`                              Temporary mount point

  `/media`                            Mount points for removable media

  `/usr`                              User applications and supporting
                                      files

  `/etc`                              System and application
                                      configuration files

  `/boot`                             Boot files, including Linux kernels
                                      and GRUB files

  `/opt`                              Optional/third-party application
                                      software

  `/home`                             Home directories for regular users

  `/tmp`                              Temporary files; contents may be
                                      cleared on reboot
  -----------------------------------------------------------------------

## 3. Basic Commands

  Command      Meaning
  ------------ --------------------------------------------------------
  `pwd`        Print current working directory
  `ls`         List files and directories
  `ls -la`     List all entries, including hidden files, with details
  `uname`      Show kernel/system name
  `uname -r`   Show kernel release/version
  `cd DIR`     Change directory
  `cd ..`      Move to parent directory
  `cd ~`       Go to the current user's home directory
  `clear`      Clear terminal screen
  `whoami`     Show current username
  `history`    Show previously entered commands
  `date`       Show date and time

## 4. Create Files and Directories

``` bash
mkdir projects                 # Create one directory
mkdir dir1 dir2 dir3           # Create multiple directories
mkdir -p parent/child/demo     # Create nested directory path
touch notes.txt                # Create an empty file, or update its timestamp
touch a.txt b.txt c.txt        # Create multiple files
```

**Important:** `touch` can create an empty file, but it is not a text
editor. Use `nano file.txt` or `vim file.txt` to edit text.

## 5. Copy, Remove, Move and Rename

### Copy --- `cp`

Syntax: `cp [options] SOURCE DESTINATION`

``` bash
cp file.txt backup.txt         # Copy a file
cp -r folder/ folder_backup/   # Copy a directory recursively
cp -v file.txt /tmp/           # Verbose output
cp -f file.txt destination/    # Force overwrite where permitted
```

-   `-r`: copy directories recursively
-   `-v`: show what is being copied
-   `-f`: force replacement where possible

### Remove --- `rm`

``` bash
rm file.txt                    # Delete a file
rm -r folder/                  # Delete a directory and its contents
rmdir empty_folder/            # Delete an empty directory
```

**Caution:** `rm` normally does not move files to a recycle bin. Check
the path before running it.

### Move or rename --- `mv`

``` bash
mv file.txt /tmp/              # Move a file
mv oldname.txt newname.txt     # Rename a file
mv folder/ /tmp/               # Move a directory
```

## 6. User Management

Common commands (exact options can vary slightly between Linux
distributions):

``` bash
sudo useradd ali               # Create a user
sudo passwd ali                # Set/change the user's password
id ali                         # Show user ID, group ID and groups
su - ali                       # Switch to another user
exit                           # Leave the switched-user shell
sudo userdel ali               # Delete a user
sudo userdel -r ali            # Delete user and their home directory
sudo usermod -l newname oldname  # Change a login name
```

-   Use `passwd USER` to set or change a user's password.
-   Use `id USER` to inspect account/group information.
-   `userdel -r` removes the user's home directory too; verify before
    using it.

## 7. Group Management

A group is a collection of user accounts used to manage permissions for
multiple users.

``` bash
sudo groupadd developers       # Create a group
getent group developers        # Check group entry
sudo usermod -aG developers ali  # Add user to supplementary group
sudo gpasswd -d ali developers  # Remove user from group
sudo groupdel developers      # Delete a group
```

-   `-aG` adds the user to supplementary groups while preserving
    existing supplementary memberships.
-   Group administrator/member management can also be done with
    `gpasswd`, depending on the distribution.

## 8. Linux File Permissions

Three common permission classes:

-   **Owner (`u`)** --- file owner
-   **Group (`g`)** --- users in the file's group
-   **Others (`o`)** --- everyone else

Permission symbols:

  Symbol   Meaning               Numeric value
  -------- ------------------- ---------------
  `r`      Read                              4
  `w`      Write                             2
  `x`      Execute                           1
  `-`      Permission absent                 0

Example: `-rwxr-xr--`

-   First character: file type (`-` file, `d` directory)
-   `rwx`: owner can read, write and execute
-   `r-x`: group can read and execute
-   `r--`: others can read

### Check and change permissions

``` bash
ls -l file.txt                 # Check file permissions
ls -ld folder/                 # Check directory's own permissions
chmod u+r file.txt             # Add read permission for owner
chmod g+rw file.txt            # Add read/write for group
chmod o-r file.txt             # Remove read permission from others
chmod 754 script.sh            # Set owner=rwx, group=r-x, others=r--
```

Numeric permissions are added together for each class. For example,
`7 = 4+2+1`, `5 = 4+1`, and `4 = 4`.

### Change ownership

``` bash
sudo chown ali file.txt        # Change owner
sudo chown ali:developers file.txt  # Change owner and group
sudo chgrp developers file.txt # Change group owner
```

## 9. Access Control Lists (ACL)

ACLs allow additional, more specific permissions for users or groups
beyond the basic owner/group/others permissions.

``` bash
getfacl file.txt                       # View ACL
setfacl -m u:ali:r file.txt            # Give ali read permission
setfacl -m g:developers:rw file.txt    # Give group read/write permission
setfacl -x u:ali file.txt              # Remove ali's ACL entry
setfacl -x g:developers file.txt       # Remove group's ACL entry
setfacl -b file.txt                    # Remove all extended ACL entries
```

## 10. Search Text with `grep` and Regular Expressions

`grep` searches files for lines matching a pattern.

``` bash
grep "error" app.log                  # Search for a word/string
grep "error" app.log system.log       # Search multiple files
grep -i "error" app.log               # Case-insensitive search
grep -r "error" ./logs/               # Search recursively
grep -v "error" app.log               # Show lines that do not match
grep -c "error" app.log               # Count matching lines
grep -l "error" ./*.log               # Show files with a match
grep -L "error" ./*.log               # Show files without a match
grep -n "error" app.log               # Include line numbers
grep '^Start' app.log                 # Lines starting with Start
grep 'end$' app.log                   # Lines ending with end
grep "error" app.log > matches.txt    # Redirect matches to a new file
```

Useful regular-expression anchors: - `^` matches the start of a line. -
`$` matches the end of a line.

## 11. Find Files with `find`

`find` searches for files/directories by location and conditions such as
name, type, owner, group, permissions and size.

``` bash
find ~ -type f                       # Files under home directory
find . -type f -name "*.log"         # Find log files in current tree
find . -type f -size -10M            # Files smaller than 10 MB (approx. find size units)
find . -type f -size +10M            # Files larger than 10 MB (approx. find size units)
find / -type f -perm -4000 2>/dev/null  # Files with SUID permission bit
find / -type f -perm -2000 2>/dev/null  # Files with SGID permission bit
find / -type d -perm -1000 2>/dev/null  # Directories with sticky bit
find /home -user ali                 # Files owned by ali
find /home -group developers         # Files belonging to developers group
```

Searching from `/` may require administrator privileges. `2>/dev/null`
hides permission-denied messages.

## 12. Counting and Viewing File Content

### `wc` --- Word Count

``` bash
wc -l file.txt       # Count lines
wc -w file.txt       # Count words
wc -c file.txt       # Count bytes
```

### `head` --- Beginning of a file

``` bash
head file.txt         # First 10 lines by default
head -n 20 file.txt   # First 20 lines
```

### `tail` --- End of a file

``` bash
tail file.txt         # Last 10 lines by default
tail -n 20 file.txt   # Last 20 lines
tail -f app.log       # Follow new lines as they are written
```

## 13. Archive and Compression with `tar`

An archive combines multiple files/directories into one file.
Compression can reduce storage size.

Common `tar` options: - `c`: create archive - `x`: extract archive -
`v`: verbose output - `f`: archive filename follows - `t`: list archive
contents - `z`: gzip compression - `j`: bzip2 compression - `J`: xz
compression - `-C DIR`: use a specific directory

``` bash
tar -cvf backup.tar folder/             # Create tar archive
tar -tvf backup.tar                     # List archive contents
tar -xvf backup.tar                     # Extract in current directory
tar -xvf backup.tar -C /tmp/restore/    # Extract into a target directory
tar -czvf backup.tar.gz folder/         # Create gzip-compressed archive
tar -xzvf backup.tar.gz                 # Extract gzip archive
tar -cjvf backup.tar.bz2 folder/        # Create bzip2 archive
tar -xjvf backup.tar.bz2                # Extract bzip2 archive
tar -cJvf backup.tar.xz folder/         # Create xz archive
tar -xJvf backup.tar.xz                 # Extract xz archive
```

## 14. Job Automation: `at` and `cron`

-   **`at`** runs a job once at a specified time.
-   **`cron` / `crontab`** schedules recurring jobs.

### `at` examples

``` bash
echo "date >> $HOME/date-log.txt" | at 10:30
atq                      # List pending at jobs
atrm JOB_ID              # Remove a pending job
```

`at` service/package availability and access controls depend on the
Linux distribution.

### Cron examples

``` bash
crontab -e               # Edit current user's cron jobs
crontab -l               # List current user's cron jobs
crontab -r               # Remove current user's entire crontab
crontab -u ali -l        # List ali's cron jobs (requires suitable privileges)
```

Cron schedule format:

``` text
minute hour day-of-month month day-of-week command
```

Example --- run a script every day at 2:30 AM:

``` cron
30 2 * * * /home/ali/backup.sh
```

Be careful with `crontab -r`: it removes the whole crontab, not just one
line.

## 15. `sudo` and Administrative Privileges

`sudo` lets an authorized user run a command with another user's
privileges, commonly root. Rules are controlled through sudoers
configuration.

``` bash
sudo command
sudo visudo
```

-   Prefer `visudo` for editing sudoers files because it checks syntax.
-   A common sudoers rule for a user is `ali ALL=(ALL:ALL) ALL`.
-   A common group rule uses a leading `%`,
    e.g. `%wheel ALL=(ALL:ALL) ALL` on systems configured to use that
    group.
-   Some distributions use `sudo`; others commonly use the `wheel`
    group.
-   Avoid passwordless sudo unless there is a specific, well-understood
    need.

## 16. Networking (RHEL-style notes)

### Show network information

``` bash
ip addr                         # Show network interfaces and IP addresses
ip route                        # Show routing table
hostname                        # Show system hostname
hostnamectl set-hostname server1  # Set hostname (systemd systems)
```

### NetworkManager with `nmcli`

`nmcli` is the command-line tool for NetworkManager.

``` bash
nmcli connection show             # List connections
nmcli connection show --active    # List active connections
nmcli device status               # Show device status
nmcli connection show "citynet"   # Show one connection
nmcli connection up "citynet"     # Activate a connection
nmcli connection down "citynet"   # Deactivate a connection
nmcli connection delete "citynet" # Delete a connection
```

Example static IPv4 configuration (check the correct connection name and
interface/network values first):

``` bash
sudo nmcli connection modify "citynet" ipv4.method manual
sudo nmcli connection modify "citynet" ipv4.addresses 192.168.0.100/24
sudo nmcli connection modify "citynet" ipv4.gateway 192.168.0.254
sudo nmcli connection modify "citynet" ipv4.dns 192.168.0.254
sudo nmcli connection up "citynet"
```

-   `nmtui` provides a text-based interface for NetworkManager.
-   Connection profiles created by `nmcli`/`nmtui` are commonly stored
    under `/etc/NetworkManager/system-connections/` on RHEL-style
    systems.
-   Editing profile files manually is generally not recommended; if
    changed, NetworkManager may need to reload/reapply the
    configuration.

## 17. Quick Revision: Most-Used Commands

  Task                       Command
  -------------------------- -----------------------------
  Current directory          `pwd`
  List files                 `ls -la`
  Move between directories   `cd DIR`
  Create directory           `mkdir DIR`
  Create file                `touch FILE`
  Copy file                  `cp SOURCE DEST`
  Move/rename                `mv SOURCE DEST`
  Delete file                `rm FILE`
  Read a file                `cat FILE`
  Edit a file                `nano FILE`
  Search text                `grep "TEXT" FILE`
  Find files                 `find PATH -name "PATTERN"`
  Check permissions          `ls -l FILE`
  Change permissions         `chmod 755 FILE`
  Change owner               `chown USER FILE`
  Current user               `whoami`
  IP address                 `ip addr`
  Network connections        `nmcli connection show`
  Archive                    `tar -cvf archive.tar DIR/`
  Extract archive            `tar -xvf archive.tar`
  Follow logs                `tail -f FILE`
  Current user's cron        `crontab -l`

## Important Safety Notes

1.  Double-check paths before `rm`, `userdel -r`, `crontab -r`, or
    deleting network connections.
2.  Use `sudo` only when required and understand what the command
    changes.
3.  Networking commands can disconnect your current session if you
    modify the active connection.
4.  The uploaded PDF's text extraction did not expose every command
    shown in screenshots/illustrations. Where a command was not visible,
    examples above are standard illustrative examples, not a verbatim
    transcription of the missing image content.

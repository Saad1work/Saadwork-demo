# Linux for DevOps — Complete Notes
## Roman Urdu | Exam Preparation + Interview + Practical Commands

**Source:** [Linux for DevOps in One Shot — Shubham Londhe](https://www.youtube.com/watch?v=e01GGTKmtpc)

---

# 1. Linux Introduction

### Linux kya hai?
Linux ek open-source operating system kernel hai. Linux kernel ke saath system tools aur applications mil kar Linux operating systems banate hain.

Examples: Ubuntu, Debian, Fedora, Red Hat Enterprise Linux (RHEL).

**Linux kahan use hota hai?**
- Web servers aur cloud servers
- DevOps aur automation
- Docker aur Kubernetes
- Networking aur cybersecurity
- Supercomputers aur embedded devices

### Linux ke important components

| Component | Meaning |
|---|---|
| Kernel | Hardware aur software ke darmiyan communication manage karta hai |
| Shell | User ki commands interpret karta hai |
| Terminal | Jahan commands type karte hain |
| File System | Files aur directories organize karta hai |
| Distribution (Distro) | Linux kernel + tools + applications ka package |

**Important:** Linux aur Ubuntu same cheez nahi hain. Ubuntu, Linux kernel par based ek distribution hai.

### Linux ke advantages
1. Open-source aur customizable.
2. Server aur cloud environments mein widely used.
3. Powerful command-line interface.
4. Automation ke liye shell scripting.
5. Multi-user aur multitasking support.
6. Permissions aur access control.

### CLI vs GUI

- **CLI:** Commands type karke computer control karna.
- **GUI:** Windows, icons, menus aur mouse se computer control karna.

DevOps mein CLI important hai kyun ke servers ko remotely manage aur tasks automate kiye ja sakte hain.

---

# 2. Linux Command Syntax

Aam command ka structure:

`command [options] [arguments]`

Example:

`ls -l /home`

- `ls` = command
- `-l` = option
- `/home` = argument/path

**Exam point:** Linux commands generally case-sensitive hoti hain. `File.txt` aur `file.txt` alag files ho sakti hain.

---

# 3. Basic Linux Commands — Most Important

| Command | Kaam | Example |
|---|---|---|
| `pwd` | Current directory ka path dikhata hai | `pwd` |
| `ls` | Files aur folders dikhata hai | `ls` |
| `ls -l` | Detailed listing | `ls -l` |
| `ls -a` | Hidden files bhi dikhata hai | `ls -a` |
| `cd` | Directory change karta hai | `cd Documents` |
| `cd ..` | Ek level peeche jata hai | `cd ..` |
| `cd ~` | Home directory mein jata hai | `cd ~` |
| `clear` | Terminal screen clear karta hai | `clear` |
| `whoami` | Current username batata hai | `whoami` |
| `history` | Purani commands dikhata hai | `history` |
| `date` | Date aur time dikhata hai | `date` |
| `cal` | Calendar dikhata hai, agar installed ho | `cal` |
| `uname -a` | Kernel/system information | `uname -a` |

### Example: directory navigation

```bash
pwd
ls
mkdir project
cd project
pwd
cd ..
```

Is example mein pehle current location check hoti hai, phir `project` folder create hota hai, us mein enter karte hain aur phir wapas parent directory mein aate hain.

### Important path concepts

- `/` = root directory
- `~` = current user ki home directory
- `.` = current directory
- `..` = parent directory
- `/home/saad/project` = absolute path
- `project/file.txt` = relative path, current directory ke hisaab se

---

# 4. File aur Directory Management

### Directory commands

| Command | Kaam |
|---|---|
| `mkdir folder` | Folder create karna |
| `mkdir -p a/b/c` | Parent directories ke saath nested folders banana |
| `rmdir folder` | Empty folder delete karna |
| `rm file.txt` | File delete karna |
| `rm -r folder` | Folder aur uske andar ka content delete karna |
| `cp file.txt backup.txt` | File copy karna |
| `cp -r src dest` | Directory copy karna |
| `mv old.txt new.txt` | File rename karna |
| `mv file.txt /tmp/` | File move karna |
| `touch file.txt` | Empty file create karna ya existing file ka timestamp update karna |
| `file filename` | File type identify karna |

### Practical example

```bash
mkdir linux-practice
cd linux-practice
touch notes.txt
cp notes.txt backup.txt
mv backup.txt old-notes.txt
ls -l
```

**Yaad rakho:**
- `cp` = copy
- `mv` = move ya rename
- `rm` = remove
- `mkdir` = make directory
- `touch` = file create/timestamp update

**Safety:** `rm -rf` bohat powerful command hai. Yeh files aur directories recursively aur forcefully delete kar sakti hai. Isay bina path verify kiye kabhi run na karo.

---

# 5. Files Read aur Edit Karna

| Command | Kaam |
|---|---|
| `cat file.txt` | Puri file terminal mein dikhana |
| `less file.txt` | File ko pages mein read karna |
| `head file.txt` | Pehli 10 lines dikhana |
| `head -n 5 file.txt` | Pehli 5 lines dikhana |
| `tail file.txt` | Aakhri 10 lines dikhana |
| `tail -f app.log` | Log file ki new lines live dekhna |
| `nano file.txt` | Terminal text editor |
| `wc -l file.txt` | Lines count karna |
| `sort file.txt` | Lines sort karna |
| `uniq file.txt` | Consecutive duplicate lines remove karna |

### `nano` editor
1. `nano notes.txt` se file open karo.
2. Text likho.
3. `Ctrl + O` se save karo.
4. Enter press karo.
5. `Ctrl + X` se exit karo.

**Exam question:** `head` aur `tail` mein difference?

- `head` file ki beginning dikhata hai.
- `tail` file ka end dikhata hai.

---

# 6. Linux File System Structure

Linux mein files aur directories ek hierarchical tree structure mein organized hoti hain.

| Directory | Purpose |
|---|---|
| `/` | Root of the entire file system |
| `/home` | Normal users ki home directories |
| `/root` | Root administrator ki home directory |
| `/etc` | System configuration files |
| `/var` | Logs aur frequently changing data |
| `/var/log` | System/application logs |
| `/tmp` | Temporary files |
| `/bin` | Essential user commands; many systems par `/usr/bin` se linked |
| `/sbin` | System administration commands; modern systems par merged layout ho sakta hai |
| `/usr` | Applications, libraries aur user-space programs |
| `/opt` | Optional third-party software |
| `/dev` | Device files |
| `/proc` | Kernel aur process information ka virtual filesystem |
| `/mnt` | Temporary/manual mount points |
| `/media` | Removable media mount points, jaise USB |

**Paper tip:** `/etc`, `/var/log`, `/home`, `/tmp` aur `/proc` ke purposes zaroor yaad karo.

---

# 7. Linux Permissions

Linux mein permissions decide karti hain ke kaun file ko read, modify ya execute kar sakta hai.

### Three permission types

| Permission | Symbol | Numeric value | Meaning |
|---|---|---:|---|
| Read | `r` | 4 | File read karna |
| Write | `w` | 2 | File modify karna |
| Execute | `x` | 1 | File execute karna |

### Three permission groups

- `u` = User/owner
- `g` = Group
- `o` = Others

Example:

```text
-rwxr-xr--
```

Iska matlab:
- Owner: `rwx` = read, write, execute
- Group: `r-x` = read, execute
- Others: `r--` = read only

### `chmod` — permissions change karna

```bash
chmod 755 script.sh
chmod 644 notes.txt
chmod u+x script.sh
```

**755 ka calculation:**
- Owner: `4 + 2 + 1 = 7`
- Group: `4 + 0 + 1 = 5`
- Others: `4 + 0 + 1 = 5`

Is liye `755` ka matlab owner ke paas full permissions, jabke group aur others ke paas read + execute.

**644 ka matlab:** Owner read/write; group aur others read-only.

### `chown` — ownership change karna

```bash
sudo chown saad notes.txt
sudo chown saad:developers notes.txt
```

- `chmod` = permissions change
- `chown` = owner/group ownership change

### `umask`
Nayi files aur directories banate waqt default permissions mein se kaunsi permissions remove hongi, yeh `umask` control karta hai.

### Special caution
`chmod 777` har kisi ko read, write aur execute permissions de sakta hai. Isay default solution na samjho; unnecessary access security risk hai.

---

# 8. Users, Groups aur sudo

Linux multi-user operating system hai. Different users ko different access diya ja sakta hai.

| Command | Purpose |
|---|---|
| `whoami` | Current username |
| `id` | User ID, group ID aur memberships |
| `who` | Logged-in users |
| `groups` | Current user's groups |
| `sudo command` | Authorized user ke liye elevated privileges |
| `su username` | Doosre user mein switch karna |
| `passwd` | Password change karna |
| `useradd username` | User create karna; options/distro ke mutabiq setup vary kar sakta hai |
| `usermod` | Existing user modify karna |
| `userdel username` | User delete karna |
| `groupadd groupname` | Group create karna |

### `sudo` kya hai?
`sudo` ka matlab hai authorized user ke through kisi command ko elevated privileges ke saath run karna.

Example:

```bash
sudo apt update
```

Yeh Ubuntu/Debian par package lists update karta hai.

**`sudo` aur `su` mein difference:**
- `sudo command`: Ek specific command elevated permissions ke saath run karta hai.
- `su username`: Doosre user ki identity mein switch karta hai.

**Important:** Har command ke aagay `sudo` lagana zaroori nahi. Sirf un tasks mein use karo jinhein elevated permissions ki zaroorat ho.

---

# 9. Software aur Package Management

Package manager software install, update aur remove karne mein madad karta hai.

### Ubuntu/Debian commands

```bash
sudo apt update
sudo apt upgrade
sudo apt install curl
sudo apt remove curl
sudo apt autoremove
```

| Command | Kaam |
|---|---|
| `apt update` | Available packages ki lists refresh karta hai |
| `apt upgrade` | Installed packages ko available updates par upgrade karta hai |
| `apt install package` | Package install karta hai |
| `apt remove package` | Package remove karta hai |
| `apt autoremove` | Unneeded automatically installed dependencies remove karta hai |

### Different Linux distributions

- Ubuntu/Debian: `apt`
- Fedora aur modern RHEL: `dnf`
- Older RHEL/CentOS: `yum`
- Arch Linux: `pacman`

**Paper question:** `apt update` aur `apt upgrade` mein difference?

`update` package information refresh karta hai; `upgrade` installed packages ko update karta hai.

---

# 10. Process Management

Process ek running program ki instance hoti hai.

| Command | Purpose |
|---|---|
| `ps` | Processes ki information |
| `ps aux` | Detailed process listing |
| `top` | Live process aur resource monitoring |
| `htop` | Interactive process monitor; separately install karna par sakta hai |
| `pgrep nginx` | Process IDs search karna |
| `kill PID` | Process ko signal bhejna |
| `kill -9 PID` | Forceful termination signal |
| `pkill processname` | Name/pattern ke mutabiq processes ko signal |
| `jobs` | Current shell ke background/stopped jobs |
| `bg` | Job ko background mein continue karna |
| `fg` | Job ko foreground mein lana |

### PID kya hai?
PID ka matlab Process ID hai. Operating system har process ko ek identifier deta hai.

Example:

```bash
ps aux
top
pgrep nginx
kill 1234
```

Yahan `1234` sirf example PID hai.

**Important:** `kill -9` normal first choice nahi honi chahiye. Pehle process ko normal termination ka chance do, kyun ke forceful termination cleanup ko rok sakti hai.

---

# 11. Services aur systemctl

Service background mein run hone wala program hota hai, jaise web server.

```bash
systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
```

| Command | Meaning |
|---|---|
| `status` | Service ki current state |
| `start` | Service start karna |
| `stop` | Service stop karna |
| `restart` | Service restart karna |
| `enable` | Boot par automatic start configure karna |
| `disable` | Boot par automatic start disable karna |

**Difference:**
- `start` abhi service start karta hai.
- `enable` future boot par automatic start configure karta hai.
- Dono ek hi cheez nahi hain.

Har Linux environment mein systemd available nahi hota. Containers aur WSL mein service management ka behavior different ho sakta hai.

---

# 12. System Information aur Resource Monitoring

| Command | Purpose |
|---|---|
| `uname -a` | Kernel/system details |
| `hostname` | System ka hostname |
| `uptime` | System kitni der se run ho raha hai aur load |
| `free -h` | RAM aur swap usage |
| `df -h` | Mounted filesystems ki disk space |
| `du -sh folder` | Folder ka approximate disk usage |
| `lsblk` | Block devices aur disks |
| `lscpu` | CPU details |
| `date` | System date/time |
| `dmesg` | Kernel ring buffer messages |

### `df` vs `du`

- `df -h`: Filesystem mein kitni disk space available/used hai.
- `du -sh folder`: Particular folder kitni disk space use kar raha hai.

### RAM vs Disk
- **RAM:** Running applications ka active working memory.
- **Disk:** Long-term storage, jaise SSD/HDD.

---

# 13. Networking Commands

Networking Linux aur DevOps ka important part hai.

| Command | Purpose |
|---|---|
| `ip addr` | Network interfaces aur IP addresses |
| `ip route` | Routing table |
| `ping example.com` | Network reachability test |
| `curl https://example.com` | HTTP request ya URL se data access |
| `wget URL` | Network se file download |
| `ss -tulpn` | Listening sockets aur ports; kuch details ke liye elevated permissions chahiye ho sakti hain |
| `dig example.com` | DNS lookup; tool installed hona chahiye |
| `nslookup example.com` | DNS query |
| `traceroute example.com` | Network path trace; installation/permissions vary kar sakti hain |
| `ssh user@server` | Remote machine par secure login |
| `scp file.txt user@server:/tmp/` | SSH ke through file copy |

### IP address kya hai?
IP address network par device/interface ko identify aur address karne ke liye use hota hai.

Example:

```bash
ip addr
ip route
ping -c 4 example.com
curl -I https://example.com
ss -tulpn
```

`ping -c 4` Linux par 4 requests bhejta hai.

### DNS kya hai?
DNS domain names ko IP addresses se resolve karne mein help karta hai.

Example: `example.com` ka IP discover karna.

### Ports kya hain?
Port numbers network connections mein services ko identify karte hain.

Common examples:
- SSH: TCP 22
- HTTP: TCP 80
- HTTPS: TCP 443
- DNS: port 53 (UDP aur TCP dono use ho sakte hain)

### `curl` vs `wget`
- `curl`: HTTP APIs, requests, headers aur data transfer ke liye useful.
- `wget`: Files download karne ke liye commonly use hota hai.

### SSH kya hai?
SSH (Secure Shell) remote computer/server par encrypted connection ke through commands run karne deta hai.

```bash
ssh username@server-ip
```

Example mein `username` aur `server-ip` ko apni actual server details se replace karna hota hai.

---

# 14. Pipes aur Redirection

Yeh concepts command-line work aur DevOps troubleshooting mein bohat important hain.

### Pipe `|`
Ek command ka output doosri command ko input deta hai.

```bash
ps aux | grep nginx
```

Pehli command processes show karti hai; `grep nginx` un lines ko filter karta hai jin mein `nginx` ho.

### Redirection

```bash
echo "Hello Linux" > notes.txt
echo "Second line" >> notes.txt
cat notes.txt
```

- `>` = file mein output likhta hai; existing content overwrite hota hai.
- `>>` = file ke end par output add karta hai.
- `<` = file se input leta hai.
- `2>` = standard error ko redirect karta hai.

Example:

```bash
ls /nonexistent 2> error.log
```

Yeh error message ko `error.log` mein redirect karta hai.

**Exam question:** `>` aur `>>` mein difference?  
`>` existing content overwrite karta hai, jabke `>>` content append karta hai.

---

# 15. grep, find, awk aur sed

Yeh commands log analysis aur text processing mein important hain.

### `grep` — text search

```bash
grep "error" app.log
grep -i "error" app.log
grep -n "error" app.log
grep -r "TODO" .
```

- `grep`: Matching lines search karta hai.
- `-i`: Case-insensitive search.
- `-n`: Line numbers show karta hai.
- `-r`: Directories mein recursively search karta hai.

### `find` — files locate karna

```bash
find . -name "*.log"
find /tmp -type f
find . -type d
```

- `.` = current directory.
- `-type f` = files.
- `-type d` = directories.
- `-name "*.log"` = `.log` par end hone wale names.

### `awk` — structured text process karna

```bash
awk '{print $1}' file.txt
```

Yeh har line ka pehla whitespace-separated field print karta hai.

```bash
awk '{print $1, $3}' file.txt
```

Pehla aur teesra field print karta hai.

### `sed` — stream editor

```bash
sed 's/old/new/' file.txt
```

Har line mein pehli matching `old` occurrence ko `new` se replace karke output deta hai.

```bash
sed 's/old/new/g' file.txt
```

Har line mein matching occurrences replace karta hai.

By default, `sed` original file ko modify nahi karta; output print karta hai.

### `grep` vs `find` vs `awk` vs `sed`

| Command | Main purpose |
|---|---|
| `grep` | Text search/filter |
| `find` | Files/directories locate karna |
| `awk` | Fields aur structured text process karna |
| `sed` | Text stream edit/replace karna |

---

# 16. File Transfer Commands

### `scp`

```bash
scp notes.txt user@server:/tmp/
```

Local file ko remote server par copy karta hai.

Remote se local:

```bash
scp user@server:/tmp/notes.txt .
```

### `rsync`

```bash
rsync -av source/ destination/
```

Files/directories ko efficiently synchronize karne ke liye use hota hai. Remote servers ke saath bhi use ho sakta hai.

**Difference:** `scp` straightforward file copy ke liye useful hai; `rsync` repeated synchronization aur changed data transfer ke liye zyada flexible hai.

---

# 17. Disk Management aur LVM

### Basic storage terms

- **Disk:** Physical ya virtual storage device.
- **Partition:** Disk ka logical division.
- **Filesystem:** Data ko files/directories mein organize karne ka format.
- **Mount point:** Directory jahan filesystem accessible hota hai.
- **LVM:** Logical Volume Manager; flexible storage management.

### LVM ke three core concepts

1. **PV — Physical Volume:** Disk ya partition jo LVM ke liye prepare kiya gaya ho.
2. **VG — Volume Group:** Multiple physical volumes ka storage pool.
3. **LV — Logical Volume:** Volume group se allocate kiya gaya logical storage volume.

Simple relationship:

`Disk/Partition → PV → VG → LV → Filesystem → Mount Point`

### LVM ke advantages
- Storage ko flexible tareeqay se allocate karna.
- Supported configurations mein logical volumes extend karna.
- Multiple physical volumes ko pool mein combine karna.
- Storage management ko simplify karna.

Common inspection commands:

```bash
lsblk
df -h
sudo pvs
sudo vgs
sudo lvs
```

`pvs`, `vgs` aur `lvs` LVM tools installed hone par available hoti hain.

**Important:** LVM configuration commands disk data ko affect kar sakti hain. Practice ke liye virtual machine ya test disk use karo, production disk par bina backup ke experiment na karo.

---

# 18. Firewall aur Security Basics

### UFW
UFW ka full form Uncomplicated Firewall hai. Ubuntu par firewall rules manage karne ka simple tool hai.

```bash
sudo ufw status
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
```

SSH connection ko protect karne ke liye firewall enable karne se pehle confirm karo ke SSH access allow hai; warna remote access lock out ho sakta hai.

### Security best practices
- Strong passwords aur SSH keys use karo.
- Unnecessary ports open na rakho.
- Minimum required permissions do.
- Regular security updates install karo.
- Logs monitor karo.
- Secrets/passwords GitHub par upload na karo.
- Unknown scripts ko root privileges ke saath blindly execute na karo.

---

# 19. Shell Scripting Basics

Shell script ek file hoti hai jisme multiple shell commands likh kar automate ki ja sakti hain.

Example `hello.sh`:

```bash
#!/bin/bash

echo "Hello Linux"
pwd
date
```

Run karne ka tareeqa:

```bash
chmod +x hello.sh
./hello.sh
```

### Important concepts
- `#!/bin/bash` = shebang; script ko Bash interpreter se run karne ke liye.
- `echo` = text output.
- Variables:

```bash
name="Saad"
echo "$name"
```

- Condition:

```bash
if [ -f notes.txt ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

- Loop:

```bash
for i in 1 2 3
do
    echo "$i"
done
```

**DevOps mein use:** Backups, deployments, repetitive commands aur routine system tasks automate karna.

---

# 20. Shutdown aur Reboot

```bash
sudo reboot
sudo shutdown -h now
```

- `reboot` = system restart.
- `shutdown -h now` = system ko abhi shutdown karne ki request.

Remote server par yeh commands run karne se pehle confirm karo ke restart/shutdown allowed hai aur doosre users/services affect nahi honge.

---

# 21. Most Important Differences — Exam Revision

| Question | Answer |
|---|---|
| Linux vs Ubuntu | Linux kernel hai; Ubuntu Linux-based distribution hai |
| CLI vs GUI | Text commands vs graphical interface |
| `pwd` vs `ls` | Current path vs directory contents |
| `cp` vs `mv` | Copy vs move/rename |
| `rm` vs `rmdir` | Files/recursive removal vs empty directory removal |
| `>` vs `>>` | Overwrite vs append |
| `df` vs `du` | Filesystem space vs directory/file usage |
| `chmod` vs `chown` | Permissions vs ownership |
| `sudo` vs `su` | Elevated command vs user switch |
| `apt update` vs `apt upgrade` | Refresh package lists vs upgrade packages |
| `ps` vs `top` | Process snapshot vs live monitoring |
| `kill` vs `kill -9` | Requested signal vs forceful termination |
| `start` vs `enable` | Abhi start vs boot par automatic start |
| `grep` vs `find` | Text search vs file location |
| `curl` vs `wget` | General data transfer/API requests vs file downloading |
| PV vs VG vs LV | Physical volume vs storage pool vs logical volume |
| RAM vs disk | Temporary working memory vs persistent storage |
| Absolute vs relative path | Root se complete path vs current location ke reference se path |

---

# 22. Practice Questions — Paper Preparation

## Short questions

1. Linux kya hai?
2. Kernel aur shell mein kya difference hai?
3. Linux distribution kya hoti hai? Do examples do.
4. `pwd` command ka use kya hai?
5. Hidden files kaise display karte hain?
6. `sudo` kyun use hota hai?
7. `chmod 755` ka kya matlab hai?
8. `grep` aur `find` ka difference likho.
9. `df -h` aur `du -sh` kya show karte hain?
10. SSH kya hai?
11. DNS aur IP address kya hain?
12. Pipe aur output redirection kya hain?
13. PID kya hota hai?
14. `apt update` aur `apt upgrade` mein difference likho.
15. LVM mein PV, VG aur LV define karo.

## Command-writing questions

**Q1. Current directory check karne ki command likho.**

Answer: `pwd`

**Q2. `project` naam ka folder banao.**

Answer: `mkdir project`

**Q3. `notes.txt` ki copy `backup.txt` naam se banao.**

Answer: `cp notes.txt backup.txt`

**Q4. File mein `error` search karo.**

Answer: `grep "error" app.log`

**Q5. Current directory mein saari `.log` files search karo.**

Answer: `find . -name "*.log"`

**Q6. RAM usage check karo.**

Answer: `free -h`

**Q7. Disk space check karo.**

Answer: `df -h`

**Q8. Running processes dekho.**

Answer: `ps aux`

**Q9. File ki first five lines dekho.**

Answer: `head -n 5 notes.txt`

**Q10. File ko read-only permissions (owner, group aur others) ke liye configure karo.**

Answer: `chmod 444 notes.txt`

## Long questions

1. Linux architecture aur components explain karo.
2. Linux file system hierarchy explain karo.
3. File permissions aur `chmod` numerical notation examples ke saath explain karo.
4. Linux networking commands aur unke uses explain karo.
5. Process management aur `systemctl` commands explain karo.
6. `grep`, `find`, `awk` aur `sed` ka comparison karo.
7. LVM architecture ko PV, VG aur LV ke saath explain karo.
8. Shell scripting kya hai? Ek simple script likho.
9. Linux package management explain karo.
10. Linux security aur user/group permissions discuss karo.

---

# 23. One-Page Quick Revision

```bash
# Navigation
pwd
ls -la
cd ..
cd ~

# Files and folders
mkdir project
touch notes.txt
cp notes.txt backup.txt
mv backup.txt old.txt
rm old.txt
rmdir empty-folder

# Read and search
cat notes.txt
head -n 5 notes.txt
tail -f app.log
grep -i "error" app.log
find . -name "*.log"

# Permissions and users
whoami
id
chmod 755 script.sh
chown user:group notes.txt
sudo command

# System monitoring
uname -a
uptime
free -h
df -h
du -sh .
ps aux
top
systemctl status nginx

# Networking
ip addr
ip route
ping -c 4 example.com
curl -I https://example.com
ss -tulpn
ssh user@server
scp file.txt user@server:/tmp/

# Package management — Ubuntu/Debian
sudo apt update
sudo apt upgrade
sudo apt install curl

# Text processing
grep "error" app.log
awk '{print $1}' file.txt
sed 's/old/new/g' file.txt

# LVM inspection
lsblk
sudo pvs
sudo vgs
sudo lvs
```

---

## Final study strategy

1. **Pehle:** Linux basics, filesystem, navigation aur file commands.
2. **Phir:** Permissions, users/groups, `sudo` aur package management.
3. **Uske baad:** Processes, networking, pipes, `grep`, `find`, `awk`, `sed`.
4. **Aakhir mein:** LVM, shell scripting aur security.
5. Har command ko Ubuntu terminal ya WSL mein khud run karo. Definitions ke saath command ka output bhi samjho.

**Paper ke liye sab se important:** Definitions, syntax, command output, permissions ke numerical values, aur similar commands ke differences. Yeh notes tumhari preparation ka base hain; apne teacher ke syllabus aur class slides ko bhi priority dena.
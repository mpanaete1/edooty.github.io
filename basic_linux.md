<h1>Basic Linux Commands</h1>

 [Home](index.html)

<h6>For systadmin/advanced Linux: <a href=ex200.html>EX200</a></h6>

[toc]

## :wave: Introduction to Linux



Linus Torvalds wrote the first Linux kernel in 1991. Linux is an open source operating system made up mostly of the following layers:

- **Kernel** - Core component of the Operating System. It provides and manages computer resources. Responsible for process, memory, and device management

- **Desktop environment** - GNOME, KDE's Plasma, MATE, and XFCE. Distributions (distros) like Debian, Fedora, etc. use different desktop environments

- **Daemons** - programs that run in the background of the operating system (like system processes in windows)

- **User Applications** - Applications user installs 

  

| GUI      | Filesystems | Shell | Libraries           |
| -------- | ----------- | ----- | ------------------- |
| x11      | ext3        | bash  | libc vs glibc       |
| unity    | ext4        | zsh   | uclibc vs musl_libc |
| gnome    | xfs         | tsh   |                     |
| kde      | jfs         | csh   |                     |
| lxde     | reiserfs    | sh    |                     |
| xfce     | btrfs       | korn  |                     |
| cinnamon | zfs         | fish  |                     |
| cli      | hfs         |       |                     |

<u>Five Main Distributions</u>

| Debian    | Arch | Slackware | RedHat | Android |
| --------- | ---- | --------- | ------ | ------- |
| Ubuntu    |      |           | CentOS |         |
| Kali      |      |           | Fedora |         |
| Mint      |      |           |        |         |
| Backtrack |      |           |        |         |



## :thinking: Understanding your Environment

<a href="basic_linux.html">Top</a>



| Command         | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| `uname -a`      | determine OS, Version, and Distribution                      |
| `whoami`        | shows what user you are logged in as                         |
| `id`            | shows detailed information about a user. Also shows group ids and groups you are in |
| `echo $PATH`    | prints the environment path                                  |
|                 | add directory/file to path : `export PATH=$PATH;<directory/file to add>` |
| `hostname`      | shows hostname of machine                                    |
|                 | locations:   `/etc/hosts   /etc/hostname   /etc/sysconfig/network` |
| `date`          | shows current date. There are several options for displaying the date |
|                 | show MM/DD/YYYY H:M:S :  `date +%D\ %T`                      |
| `w`             | show who is logged in TTY, Login Time, Idle, and what they are doing |
| `uptime`        | check system uptime                                          |
| `Absolute Path` | when navigating to or viewing a file use full path starting with root (/) |
|                 | example:  `cat /home/user/Documents/files/file1.txt`         |
| `Relative Path` | as opposed to absolute, you would be in the directory of the file you wish to interact with |
|                 | example: `cd /home/user/Documents/files/ `   `cat file1.txt` |



<u>Basic Permissions on a file/directory</u> 

`ls -latr file.txt`

**-rw-r--r--    1   user    group    1389    Mon    Day    00:00    file.txt**



| Input     | Description                                                  |
| --------- | :----------------------------------------------------------- |
| -         | file type :   **-** (file), **d** (directory), **l** (link), **b** (block device), **s** (socket) |
| rw-r--r-- | permissions                                                  |
| 1         | number of links                                              |
| user      | user that owns the file                                      |
| group     | group that owns the file                                     |
| size      | size of the file in kilobytes (`ls -h`for human readable)    |
| Mon/Day   | month and day file/directory was created/modified            |
| 00:00     | time the file was created/ last modified                     |
| file.txt  | file name                                                    |



<u>Command Prompt</u>

**student@workstation:~ $**



| Input       | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| student     | current user                                                 |
| workstation | hostname                                                     |
| ~           | current directory  ~ is the current users home directory     |
| $           | regular user permissions ,  #  would be superuser(root) permissions |

---



## :question: Help

<a href="basic_linux.html">Top</a>

Get help with most commands by typing `--help` after a command or use man pages `man <command>`

| Command   | Description                                                  |
| --------- | ------------------------------------------------------------ |
| `man`     | manual pages (help) for most commands                        |
|           | when inside man you can type / to search for a specific term hit enter and then type (n) to move to next found result |
| `--help`  | run after a command for a brief help summary   `cat --help`  |
| `whatis`  | show man pages and one-liner summary   `whatis <command>`    |
| `apropos` | search for a feature and get a list of tools for that feature  (man -k does the same thing)   `apropos <command>` |
| `info`    | provides information about a particular command   `info <command>` |

---



## :globe_with_meridians: Navigation and Exploring

<a href="basic_linux.html">Top</a>

| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| `pwd`   | Print working directory                                      |
| `ls`    | List files in a directory (lowercase L)                      |
|         | `l` - long listing                                           |
|         | `a` - show hidden files                                      |
|         | `t` - sort by modified time newest first                     |
|         | `r` - reverse order while sorting                            |
|         | `d` - show directory info                                    |
|         | `h` - human readable size                                    |
| `file`  | determine a files type (jpg, bin, ASCII, tar, gzip)  `file <file>` |
| `cd`    | Change directory. `cd` by itself (no options) will always take you to the current users home directory |
|         | `cd ..`    takes you back (up) to the parent directory       |



<u>View the contents of a file:</u>

| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| `cat`   | View contents of a file                                      |
| `less`  | scroll forward and backward through a file                   |
| `more`  | View contents of a file one page at a time                   |
| `head`  | View the first 10 lines of a file (10 lines default)  `-n #` to specify number of lines to show |
| `tail`  | View the last 10 lines of a file (10 lines default)   `-n #` to specify number of lines to show |
| `grep`  | print lines matching a pattern                               |
|         | `grep root /etc/passwd` will show you only lines that include root in the /etc/passwd file |
|         | you can use regular expression with `grep -e/E` using -e is the same as using the command `egrep`. also used to provide several search terms |
|         | Regular Expression: `^root` begins with root , `root$` ends in root, `.` matches any single character, `[ec]` will match a group of characters. Much more covered [here](https://linuxize.com/post/regular-expressions-in-grep/) |

---



## :open_file_folder: Manipulating Files and Directories

<a href="basic_linux.html">Top</a>

| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| `cp`    | copies a file/directory from one location to another  `cp <filename> <destination>` |
|         | `cp -r`    copy full directories                             |
| `mv`    | moves or renames a file/directory `mv <filename> <destination>` |
|         | mv can also be used to rename a file `mv file1.txt file1_newname.txt` |
| `mkdir` | create/make a new directory                                  |
|         | `mkdir -p`  creates all directories including parent directories if they do not exist |
| `rm`    | remove a file   `rm <filename>`                              |
|         | `rm -r <directory>`  remove a directory                      |
|         | `rm -rf <filename>/<directory>` force removal of file and/or directory |
|         | You may use the * as a wildcard, meaning all or everything. `rm ~/Documents/files/*`  will delete every file in the directory |

---



## :notebook: Text Editors

<a href="basic_linux.html">Top</a>

| Text Editor | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| `vim`       | comprehensive text editor with a big learning curve but worth it. `vim <file>`  [Vim Cheatsheet](https://vim.rtorr.com/) |
|             | `esc`  command mode                                          |
|             | `i`  enter insert mode                                       |
|             | `:wq!`   save and quit                                       |
|             | `:q!`  quit without saving                                   |
|             | `dd` delete a single line                                    |
|             | `:set nu`  add line numbers                                  |
|             | `u`  undo/redo                                               |
|             | `yy`  copy a line                                            |
|             | `p`  paste a line                                            |
|             | `v`  enter visual mode (easier to select and delete)         |
| `nano`      | easy text editor   `nano <file>`                             |
|             | `ctrl + o`   writes/saves file                               |
|             | `ctrl + x`   exit nano                                       |
| `gedit`     | will open a notepad/wordpad gui to edit/create files         |

---



## :family: Creating Users and Groups

<a href="basic_linux.html">Top</a>

| Command                        | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `useradd <options> <username>` | create a new user                                            |
|                                | `-d` set home folder     default: `/home/<username>`         |
|                                | `-s` specify shell             `/bin/bash /bin/sh /bin/fish` |
|                                | `-c "Comment"` add a comment for new user                    |
|                                | `-g <group>` specify primary group                           |
|                                | `-G <additional group>` add supplementary/additional groups  |
|                                | `-u <number>` specify user ID                                |
| `passwd <username>`            | set/change password for specific user                        |
| `usermod <username>`           | modify a user account                                        |
|                                | `usermod -a -G <supplementary group> <username>` add an existing user to another group |
| `groupadd  <groupname>`        | create a new group                                           |
|                                | `-g <number>` specify group id                               |
| `chage <username>`             | show password policy for a user                              |
|                                | `-d` set number of days since password was changed. set to 0 to have user change password on first log in |
|                                | `-m` minimum days between password changes                   |
|                                | `-M` maximum days password is valid                          |
|                                | `-W` set number of days of warning before a password change is required |



<u>All users on the system have an entry in /etc/passwd:</u>

**student:X:1000:1000:New Student User:/home/student:/bin/bash**

| Section          | Description                         |
| ---------------- | ----------------------------------- |
| student          | username                            |
| x                | password is stored in `/etc/shadow` |
| 1000             | user ID                             |
| 1000             | group ID                            |
| New Student User | user comment                        |
| /home/student    | home directory                      |
| /bin/bash        | users shell                         |



<u>Passwords are stored (encrypted) in the `/etc/shadow` file:</u>

**student**:$6$LKj8SL2rdS$lkSl38Slnww08slsks3LS:17736:0:99999:7:::

| Section               | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| student               | username                                                     |
| $6$                   | encryption type                                              |
| LKj8SL2rdS$           | password salt                                                |
| lkSl38Slnww08slsks3LS | encrypted Password                                           |
| 17736                 | the date when the password was last changed, number of days since January 1, 1970 (epoch date) |
| 0                     | minimum password age                                         |
| 99999                 | maximum password age                                         |
| 7                     | warning period                                               |
| last three            | inactivity period, expiration date, Unused                   |

<u>Encryption Types:</u>

$1$ – MD5

$2a$ – Blowfish

$2y$ – Eksblowfish

$5$ – SHA-256

$6$ – SHA-512

---



## :mag: Locating Files and Searching

<a href="basic_linux.html">Top</a>

| Command             | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `find`              | find a file or directory `find <search location> <options> <search term>` |
|                     | `find /` searches in the root directory                      |
|                     | `-type`  searches for a type : f file  d directory  b block device |
|                     | `-iname` search case insensitive                             |
|                     | `-user` search files owned by a specific user                |
|                     | `-group` search files owned by a specific group              |
|                     | `-perm` search for files with specific permission set (octal format, see permissions section) |
|                     | `-size #c` search for files with a specific size (c for bytes, M for megabytes, G for Gigabytes) |
| `locate <filename>` | locates a file or directory. You may need to `updatedb`      |

---



## :page_facing_up: Processes

<a href="basic_linux.html">Top</a>

| Command  | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `ps`     | show running processes `ps -elf |grep <username or program>` |
|          | `ps -elf `             `e`  all processes, `l`  long format , `f`  full-format |
| `top`    | live view of running processes                               |
|          | `c` sort by CPU usage                                        |
|          | m sort by memory usage                                       |
|          | `k` to kill a process followed by process id (PID) then `<enter>` |
|          | `r` to renice using PID                                      |
| `renice` | control/set the priority of a process  `renice -n <value> <PID>` |
|          | values range from -20 to +19 priority (-20 highest, +19 lowest, 0 default) |
| `pidof`  | get PID of a program   `pidof <process name>`                |
| `kill`   | kills a process using signals. Get a list of signals and their corresponding values `man 7 signal` |
|          | `kill <signal/number> <PID>`                                 |
|          | Kill Signal - `kill -9 <PID>`  same as `kill SIGKILL <PID>`  |

---



## :no_entry: Permissions		

<a href="basic_linux.html">Top</a>

Each file/directory can have <u>r(read)</u>, w(write), and <u>x(execute)</u> permissions

When doing a long listing `ls -l` on a file you can see what permissions are on that file. Use `ls -ld` to see permissions on directories



**-rwxrw-r--   1    student    class1     1389     Mon    Day      00:00      file.sh**



| Permission | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| rwx        | the first permissions would be for <u>owner</u> permissions (student) |
| rw         | the second permissions would be for <u>group</u> permissions (class1) |
| r          | the third permissions would be for <u>all others</u> (not the owner or part of the group) |

In the example file (file.sh) above the following permission would apply

| User/Group/Others                                        | Permissions                                                  |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| The user student                                         | Read, Write/Edit, and Execute the file.sh script             |
| The group class1                                         | Read, Write/Edit the file.sh script but would not be able to execute/run the file.sh script |
| All Others (not the user student or in the group class1) | Would only be allowed to read the contents of the file.sh script |

​	

| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| `chmod` | change permissions of a file.  `chmod <octal or letters> <file>` |
|         | When changing permission on a file you can use **letters (rwx)** or **octal (755)** to represent what permissions you want on a file |

<u>Octal Numbers</u> 

 R W X are represented as 4 2 1 respectively 

| Octal | Permission |
| ----- | ---------- |
| 7     | RWX        |
| 6     | RW         |
| 5     | RX         |
| 4     | R          |
| 3     | WX         |
| 2     | W          |
| 1     | X          |

 `chmod 764 file.sh` 

- 7 would be for the user permissions

- 6 for group permissions 

- 4 for all other permissions.

  

<u>Letter Representation</u>

- `u` for user
- `g` for group
- `o` for others

use r w x  to specify  permissions. use `+` to add, `-` to remove permissions

​	 `chmod u+rwx file.sh`                        this will apply r w x permissions for the user.

​	 `chmod g-x file.sh`  			              this will remove x permissions for the group.

​	 `chmod u+rwx,g+rw,o+r file.sh`     this will apply r w x for the user, r w for the  group, and r for others.

Additional permissions [here](rh124.html)



| Command | Description                                                  |
| ------- | ------------------------------------------------------------ |
| `chown` | change ownership of a file  `chown <user>:<group> <filename/directory>` |
|         | `chown root:wheel file.sh` changes the owner of the file.sh to root and the group owner to wheel |
|         | `chown :wheel file.sh`    would only change group ownership  |
|         | `chown root: file.sh`      would only change user ownership  |

---



## :zap: Networking

<a href="basic_linux.html">Top</a>

| Command      | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `ifconfig`   | show network configurations such as interfaces, ipv4/ipv6 address, netmask, broadcast |
|              | most distributions are moving to `ip addr` instead of `ifconfig` |
| `ip neigh`   | show links connected to host (similar to arp -a)             |
| `ip route`   | show routing table (how your network is routed)              |
|              | can also use `route` for a cleaner output                    |
| `traceroute` | show the route a packet takes to a specific host `traceroute <URL/IP>` |
| `netstat`    | show network socket information  `netstat -auntp`            |
|              | `a` show all                                                 |
|              | `u` show udp connections                                     |
|              | `t` show tcp connections                                     |
|              | `n` show numeric only, no host name resolution               |
|              | `p` show PID and program                                     |
| `ss`         | similar to netstat, more functionality                       |
|              | `ss -auntp`  this would give a similar output as netstat -auntp |
|              | `ss -o state established '( dport = :ssh or sport = :ssh )'` specify state and destination/source ports |
|              | `-o` show timer information (state=all,established,listening,time-wait,closed ) |
|              | `'(<parameters go here such as dport = :ssh)'`               |
|              | `'(src 192.168.1.24 or dst 192.168.1.24)'` specify source and destination IPs |

---


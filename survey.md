<h1>Survey</h1>

[Home](index.html)

[toc]

## *NIX

| Command                        | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| `ifconfig`                     | network info, use `ip addr` for most distrobutions           |
| `date; date -u`                | get date/time information                                    |
| `uname -a`                     | get kernel/build information.  cat`/etc/*release*`           |
| `ls -latr /`                   | look for anything weird in root                              |
| `ls -latr /tmp`                | look for anything weird in /tmp                              |
| `ls -latr .`                   | look for anything weird in current directory                 |
| `ls latr ..`                   | look for anything weird in parent directory                  |
| `sudo ls -latr /root`          | look for anything weird in /root                             |
| `ps -elf`                      | look for any suspicous processes                             |
| `netstat -auntp`               | look for any suspicous network connections                   |
| `w`  and `last`                | look for any other loged in users                            |
| `ls -latr /var/spool/cron`     | check individual users crontabs. tail -n 1000 files in /var/spool/cron |
| `ls -la /etc/cron.*`           | check for any scheduled jobs                                 |
| `cat /etc/crontab`             | check for scheduled jobs                                     |
| `df -h and lsblk`              | check for any devices that may be out of place or extra      |
| `ls -latr /var/*acc*`          | check for process accounts (logs everything)                 |
| `ls -latr /var/log/`           | check for any logs of suspicous bins                         |
| `ls -la /etc/*syslog*`         | check for remote logging. cat all rsyslogs*                  |
| `sestatus || getenforce`       | check status of selinux                                      |
| `sudo cat /root/.bash_history` | check for any command history from root                      |
| `cat ~/.bash_history`          | check for any command history from user                      |

check for specific users indiviudual scheduled jobs

```
for user in $(cut -f1 -d: /etc/passwd); do echo "###### $user crontab is:"; cat /var/spool/cron/{crontabs/$user,$user} 2>/dev/null; done 
```

 look for any logs that where created since you loged in. change -6 to how long you have been on the box

```
find / \( -path /proc -prune -o -path /sys -prune \) -o -mmin -6 -type f -print | xargs ls -latr
```



---



## Windows

<a href="survey.html">Top</a>

| Command                                                      | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `ipconfig /all`                                              | network information                                          |
| `date /t`                                                    | date of machine                                              |
| `time /t`                                                    | time of machine                                              |
| `tasklist /V` and `tasklist /SVC`                            | look for any weird tasks running (processes)                 |
|                                                              | `wmic process get name,processid,parentprocessid,executablepath,sessionid` |
| `auditpol /get /category:*`                                  |                                                              |
| `netstat /anob`                                              | look for strange connections                                 |
| `netsh advfirewall show all profiles`                        | show firewall profiles, see if any may interfere with objectives |
| `net share`                                                  | look for any shares on box                                   |
| `reg query hklm\software\microsoft\windows\currentversion\run` | look for programs running at startup                         |
| `reg query hklm\software\microsoft\windows\currentversion\runonce` | look for programs running once at startup                    |
| `reg query hklm\software`                                    | look for any weird software installed                        |
| `at`                                                         | replaced with `schtasks` run it anyways                      |
| `schtasks /query /v`                                         | look for any scheduled tasks. run without the `/v` for cleaner output |
| `dir /o:d /t:w c:\`                                          | look for any weird files in c:\                              |
| `dir /o:d /t:w c:\windows\temp`                              | look for any weird files in c:\windows/temp                  |
| `dir /o:d /t:w c:\windows\`                                  | look for any weird files in c:\windows                       |
| `dir /o:d /t:w c:\windows\system32`                          | look for any weird files in  c:\windows\system32             |
| `dir /o:d /t:w c:\windows\system32\winevt\logs`              | look for any weird files in c:\windows\system32\winevt\logs  |
| `wevtutil qe security /c:25 /rd:true /f:text`                | look for any logs in security event                          |
| `query user`                                                 | look for any loged in users                                  |

---



## Unexpected OS

<a href="survey.html">Top</a>

Research the below commands for the given unexpected OS and confirm before running

- Research how to identify IP address
- Research how to identify Operating System
- Research how to identify routes
- Research how to identify network connections
- Research how to identify updated logs
- Research how to identify uptime
- Research how to identify running processes
- Research how to identify common storage locations and what they contain

---




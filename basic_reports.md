<h1>Reports</h1>

[Home](index.html)

:page_with_curl:

[toc]

## Security Products

```
*****Security Product*****
Name - <>
Version - <>
Primary registry key/config file - <>
*****End of Report*****
```

###### Name and version of the product

| Nix*                                           | Windows                                                      |
| ---------------------------------------------- | ------------------------------------------------------------ |
| read the README file in bin                    | PowerShell  `get-item "c:\Program Files\Windows Defender\MpCmdrun.exe").VersionInfo` |
| `find / -name "psp name"`                      | `where /R c:\ “psp name”`                                    |
| read config file in `/etc`, usually at the top | `reg query hklm\software\<product name> /s`                  |
|                                                | `wmic path win32_product`                                    |
|                                                | `wmic path win32_product get name, version`                  |

###### Primary registry key/config file

| Nix*   | Windows                     |
| ------ | --------------------------- |
| `/etc` | `reg query hklm\softare /s` |

###### Installation Folder

| Nix*          | Windows                                  |
| ------------- | ---------------------------------------- |
| `ls /etc`     | `dir /o:d /t:w "c:\program files"`       |
| `ls /usr/bin` | `dir /o:d /t:w "c:\program files (x86)"` |

###### Directory location of logs

| Nix*                | Windows                               |
| ------------------- | ------------------------------------- |
| `ls -latr /var/log` | `where /R c:\ LOG`                    |
|                     | `dir "c:\program files\path\to\logs"` |

###### Timestamp of all log files

| Nix*                | Windows                              |
| ------------------- | ------------------------------------ |
| `ls -latr /var/log` | `dir "c:\program files\path\to\logs` |

###### Cloud Based?  yes or no

Can we read the logs? yes or no

if yes, put the most recent 5 lines of the logs in your notes

if no, why?

| Nix*                                                | Windows                                                      |
| --------------------------------------------------- | ------------------------------------------------------------ |
| google it, it also may be in the `/etc` config file | `reg query "HKEY_LOCAL_MACHINE\software\Wow6432Node\Zone Labs" /s /f cloud` |
|                                                     |                                                              |

---



## Abnormal Logging Report

<a href="basic_reports.html">Top</a>

```
*****Abnormal Logging Report*****
Name - <>
PID - <>
PPID - <>
User - <>
Location of config file - <>
Remote hostname or IP - <>
Network connections - <>
*****End of Report*****
```

###### Provide process name/options, PID, Parent ID, user

| Nix*                                   | Windows                                                     |
| -------------------------------------- | ----------------------------------------------------------- |
| `find / -iname <malware name>`         | `where /R c:\ <malware name>`                               |
| `ps -elf`                              | `wmic process get processid,parentprocessid,executablepath` |
| `ls -laR /usr/share/*/*man*/*rpcbind*` | `tasklist /SVC`                                             |
| `lsof -PRpn`                           | `tasklist /m /fi "IMAGENAME eq lsass.exe"`                  |
| `cat /proc/pid/maps`                   |                                                             |

###### Location of Config Files

| Nix*                            | Windows                               |
| ------------------------------- | ------------------------------------- |
| `ls /etc | grep <malware name>` | `reg query hklm /f  <search term> /s` |
| `ls /usr/bin`                   |                                       |

###### Remote hostname or IP

| Nix*                        | Windows         |
| --------------------------- | --------------- |
| `netstat -auntp`            | `netstat /anob` |
| `cat /etc/rsyslog.d/*.conf` |                 |

###### Network Connections

| Unix*            | Windows         |
| ---------------- | --------------- |
| `netstat -auntp` | `netstat /anob` |

---



## Malware Report

<a href="basic_reports.html">Top</a>

```
*****Malware Report*****
Name -
PID - <>
PPID - <>
User - <>
File type - <>
Supporting files - <>
Logs - <>
Persistence - <>
Description - <>
*****End of Report*****
```

###### Provide process name/options, PID, Parent ID, user

| Nix*                                   | Windows                                                     |
| -------------------------------------- | ----------------------------------------------------------- |
| ``find / -iname <malware name>`        | `where /R c:\ <malware name>`                               |
| `ps -elf`                              | `wmic process get processid,parentprocessid,executablepath` |
| `ls -laR /usr/share/*/*man*/*rpcbind*` | `tasklist /SVC`                                             |
| `lsof -PRpn`                           | `tasklist /m /fi "IMAGENAME eq lsass.exe"`                  |
| `cat /proc/pid/maps`                   |                                                             |

###### Provide file type of malware binary and supporting files

| Nix*                                                         | Windows                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `ls -la /path/to/file`                                       | `where /R c:\ baddy`                                         |
| `file /path/to/file`                                         | powershell: `get-childitem c:\ -recurse | ? {$_.lastwritetime -gt 'MM/DD/YY' -AND $_.lastwritetime -lt 'MM/DD/YY'} | select fullname` |
| `egrep logon -ri /etc/init*`                                 | `reg query hklm\software /s /f nvspcaps64`                   |
| `egrep systemf -ri /etc/rc*`                                 | `reg query hklm\software\wow6432node /s /f nvspcaps64`       |
| `egrep logon -ri /home`                                      | powershell `get-ChildItem -path HKLM:\SOFTWARE\wow6432node -Recurse | where { $_.Name -match 'nvspcaps64'}` |
| `egrep logon -ri /root`                                      | `dir /o:d /t:w /s c:\progra~1\*baddy*`                       |
| `egrep logon -ri /usr`                                       | `dir /o:d /t:w /s c:\progra~2\*baddy*`                       |
| `find /var/log -type f -mmin -90 -exec ls -trialh {} + | egrep -v "\/sys\/` | `dir /o:d /t:w /s c:\windows\*baddy*\`                       |
|                                                              | `dir /o:d /t:w /s c:\users\admin3`                           |

###### Provide any logs generated by malware

| Nix*                                                         | Windows            |
| ------------------------------------------------------------ | ------------------ |
| `ls -la /var/log` look for any new logs generated or `cat /var/log/messages` | `dir path\to\logs` |

###### Provide location and lines of any persistence mechanisms

| Nix*                 | Windows                    |
| -------------------- | -------------------------- |
| `cat /etc/crontab`   | `schtasks /query /FO list` |
| `ls -la /etc/cron.*` |                            |

###### Provide full path of malware files or support files

| Nix*                      | Windows               |
| ------------------------- | --------------------- |
| `ls -la /path/to/support` | `dir path\to\support` |

###### Provide any network connections opened/established by malware

| Nix*            | Windows         |
| --------------- | --------------- |
| `netstat -pant` | `netstat /anob` |

###### Provide any identifiable text	

| Nix*      | Windows   |
| --------- | --------- |
| `strings` | `strings` |
| `cat`     |           |

###### Provide any/all modules loaded by malware

| Nix*                       | Windows                                              |
| -------------------------- | ---------------------------------------------------- |
| `strings /proc/28046/maps` | `tasklist /m /fi "IMAGENAME eq <malware.name>"`      |
| `md5sum`                   | `certutil -hashfile C:\Windows\CompanionApp.exe MD5` |
| `sha1sum`                  | `get`                                                |
|                            | `strings`                                            |

---

<a href="basic_reports.html">Top</a>


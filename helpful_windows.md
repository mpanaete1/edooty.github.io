<h1 id='helpfulwindows'> Helpful Windows Commands</h1>

[Home](index.html)

[toc]

## Helpful Commands

| Description                 | Command                                                      |
| --------------------------- | ------------------------------------------------------------ |
| ping sweep                  | `for /I %i in (1,1,254) do @ping -n -1 -w 100 192.168.1.%i | find "Reply"` |
| find anything on the system | `where /R c:\ <*name*/.extension/search term>`               |

---



## Hashing

<a href="helpful_windows.html">Top</a>

Windows 8.1 and newer

<u>**Powershell**</u> 

<u>hash a single file or directory:</u>

`Get-FileHash ‘C:\path\to\file\[*]’ -Algorithm MD5 | Format-List`

Same as above Ignoring errors 

`Get-Filehash 'c:\path\to\folder(file)\[*]' -Algorith MD5 -ErrorAction Ignore | Format-List`



**<u>CertUtil</u>**

<u>hash a single file or directory:</u>

`certutil -hashfile <file to hash> <hashtype>`

- MD2
- MD4
- MD5
- SHA1
- SHA256
- SHA384
- SHA512

<u>hash a full directory:</u>

`for /r %f in (*) do(certutil -hashfile “%f” MD5) | file /v “hashfile command completed successfully” >> output.txt`

---



## Users and Groups

<a href="helpful_windows.html">Top</a>

| Description                         | Command                                                      |
| ----------------------------------- | ------------------------------------------------------------ |
| add user                            | `net user <username> <password> /ADD`                        |
|                                     | `net user /add <username>`  this command will prompt for the password |
| add user to a domain                | `net user <username> <password> /ADD /DOMAIN`                |
| delete user                         | `net user <username> /DELETE`                                |
| change home directory from default  | `/homedir:pathname`                                          |
| add comment to user                 | `/comment:"Content"`                                         |
| specify name of user                | `/fullname:"<name>"`                                         |
| show members of a group             | `net localgroup <group name>`                                |
| get full account details            | `net user <username>`                                        |
| add user to the administrator group | `net localgroup administrators <username> /add`              |

---



## Security Product Enumeration 

<a href="helpful_windows.html">Top</a>

#### Find Security Products

| Tool                | Command                                                      |
| ------------------- | ------------------------------------------------------------ |
| Powershell          | `Get-WmiObject -Namespace root\SecurityCenter2 -Class AntiVirusProduct` |
| Antivirus Info      | `dir /s C:\*SecurityProductInformation.ini`                  |
| Find antivirus Logs | `dir /s c:\*Logs | findstr -i antivirus`                     |



#### Find Installed Software

`reg query hklm\software`

`reg query hklm\software\wow6432node`

`dir “C:\Program Files”`

`dir “C:\Program Files (x86)”` 

`dir “C:\”`

`dir A:H “C:\”`

`dir “C:\Program Files\Common Files”`

`wmic product get Description, InstallDate, Name, Vendor, Version`

---



#### Windows Defender Enumeration

<a href="helpful_windows.html">Top</a>

`reg query "hklm\software\Microsoft\Windows Defender"`

`reg query "hklm\system\currentcontrolset\services\windefend`

`dir "C:\Program Files\Windows Defender"`

`dir "C:\ProgramData\Microsoft\Windows Defender\Support"`

`type "C:\ProgramData\Microsoft\Windows Defender\Support\*.log"`

`dir “C:\ProgramData\Microsoft\Windows Defender\Support\”`

`wevtutil qe "Microsoft-Windows-Windows Defender/Operational" /rd:false /c:25 /f:text`

---



#### Kaspersky Enumeration

`wevtutil qe "Kasperksy Event Log" /rd:false /c:25 /f:text`

---



#### McAfee

<a href="helpful_windows.html">Top</a>

`dir “C:\ProgramData\Mcafee\Managed VirusScan\Logs”`

`reg query hklm\software\McAfee`

`reg query hklm\software\Symantec\Symantec Endpoint Protection\AV\` 

`reg query hklm\software\Symantec\Symantec Endpoint Protection\CurrentVersion\Public-Opstate` 

`reg query hklm\software\Symantec\Symantec Endpoint Protection\SMC\SYLINK\SyLink\OpState\` 

---



#### Norton Enumeration

`dir “C:\Users\Public\Public Documents\Altiris”`

`dir “C:\Program Files\Altiris\Notification Server\Logs”`

`dir “C:\ProgramData\Symantec\SMP\Logs”`

`dir “C:\Program Files\Altiris\Altiris Agent\Logs”`

`dir “C:\Users\Public\Public Documents\Altiris\Altiris Agent\Logs”`

`dir “C:\ProgramData\Symantec\Symantec Agent\Logs”`

`reg query hklm\software\Symantec`

---



#### Finding other Security Products

`wevtutil qe "COMODO Internet Security CEF" /rd:false /c:25 /f:text`

`reg query hklm\software\wow6432node\Comodo`



<u>Something odd was running but is not running anymore</u>

`reg query "hkcu\Software\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Compatibility Assistant\Persisted" /S`

`reg query "hkcu\Software\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Compatibility Assistant\Store" /S`

`reg query"hkcu\Software\Microsoft\Windows\ShellNoRoam\MUICache" /S`

`dir /o:d /t:W c:\windows\prefetch`

---



## Windows Management Instrumentation Command Line Utility (WMIC)

<a href="helpful_windows.html">Top</a>

| Description                                    | Command                                                      |
| ---------------------------------------------- | ------------------------------------------------------------ |
| Get running services                           | `wmic service where "state='running'" get displayname,state, pathname,processid` |
| Get Users                                      | `wmic USERACCOUNT Get Domain,Name, Sid`                      |
| List Users (netlogin)                          | `wmic netlogin get name,numberoflogons,badpasswordcount`     |
| Running Processes                              | `wmic process get name,processid,parentprocessid,executablepath,sessionid` |
| List antivirus products                        | `wmic /namespace:\\root\securitycenter2 path antivirusproduct get displayname, productState,pathToSignedProductExe` |
| Show startup programs                          | `wmic startup list brief`                                    |
| Get list of running services                   | `wmic service where 'State="Running"' list brief`            |
| Interfaces on the system                       | `wmic nic list full`                                         |
| Computer system Info                           | `wmic computersystem list brief`                             |
| List system drives                             | `wmic volume list brief`                                     |
| Log file                                       | `wmic NTEVENT WHERE "LogFile='Security'" GET LogFile,SourceName,EventType,Message,TimeGenerated /FORMAT:list` |
| Additional details of running services         | `wmic service where ‘State="Running"’ get name,processId,installDate,pathName,StartMode,Caption` |
| Get products with version and install location | `wmic path win32_product get name, version, installlocation` |
| More detailed products with version            | `wmic product get Description,InstallDate,Name,Vendor,Version, ProcessID` |

---



## Powershell

<a href="helpful_windows.html">Top</a>

Port Scan single IP Ports (1..1024)

```
1..1024 | % {echo ((new-object Net.Sockets.TcpClient).Connect("[IP Address]",$_)) "Port $_ is open!"} 2>$null
```

IP Scan / Ping

```
foreach ($ip in 1..20) {Test-NetConnection -Port 80 -InformationLevel "Detailed" [First 3 octets].$ip}
```

Program Versions

```
Get-WmiObject Win32_Product | Select-Object Name,Version
```

Hash Full Directories

```
Get-FileHash 'C:\Program Files (x86)\path\to\directory\*' -Algorithm MD5 | Format-List
```

Log Search

```
Get-EventLog "Windows Powershell" -After (Get-Date).AddHours(-2) | where {($_.EventId -eq 400) -or ($_.EventId -eq 500)-or ($_.EventId -eq 501) -or ($_.EventId -eq 800) -or ($_.EventId -eq 4104) -or ($_.EventId -eq 4106)}
```

Enable SMB1

```
Enable-WIndowsOptionalFeature -Online -FeatureName smb1protocol
```

Start Powershell version 2

```
powershell -version 2
```

Check current Powershell version

```
$psversiontable
```

Check Windows Defender version

```
Get-MpComputerStatus
```

EventLog query (change event ID number)

```
Get-EventLog "Security" | where-object {$_.EventId =eq 4624}
```

Logs written to since you logged in

```
Get-WinEvent -ListLog * | ? {$_.lastwritetime -gt 'Tuesday, Mmm DD, YYYY H:MM:SS PM'}
```

Logs created since you logged in

```
Get-WinEvent -ListLog * | ? {$_.lastwritetime -gt 'Tuesday, Mmm DD, YYYY'}
```

Single Port Scan

```
Test-NetConnection <IP address> -Port <port>
```

Antivirus on system

```
Get-WmiObject -Namespace root\SecurityCenter2 -Class AntiVirusProduct
```

Netstat with pid and Process name

```
get-nettcpconnection | sort-object -Property state | format-table local*,remote*,state,OwningProcess, @{Name="Process";Expression={(Get-Process -Id $_.OwningProcess).ProcessName}}
```

Startup Programs

```
Get-CimInstance Win32_StartupCommand |Select-Object Name, command, Location, User |Format-List
```

Powershell Logging

`wevtutil gl "Windows PowerShell"`

`wevtUtil gl "Microsoft-Windows-PowerShell/Operational"`

`wevtutil qe "Windows Powershell" /rd:false /c:25 /f:text`

`wevtutil qe "Microsoft-Windows-PowerShell/Operational" /rd:false /c:25 /f:text`

`Get-EventLog "Windows Powershell" -After (Get-Date).AddHours(-2) | where {($_.EventId -eq 400) -or ($_.EventId -eq 500)-or ($_.EventId -eq 501) -or ($_.EventId -eq 800) -or ($_.EventId -eq 4104) -or ($_.EventId -eq 4106)}`

---



## Net Commands

<a href="helpful_windows.html">Top</a>

| **Command**      | **Description**                                              |
| ---------------- | ------------------------------------------------------------ |
| `Net Accounts`   | Update the accounts database, modify account and password settings, or display account information. |
| `Net Computer`   | Add or remove computers from the domain.                     |
| `Net Config`     | Display or change the setting for the Server or Workstation service. |
| `Net Continue`   | Restart a paused Windows service.                            |
| `Net File`       | Display a list of open shared files and file locks; this command can be used to close a shared file and remove a file lock. |
| `Net Group`      | Add, modify, delete, or display global group account information in the domain directory database. |
| `Net Help`       | Obtain a list of net commands or get help for a specific net command. |
| `Net Helpmsg`    | Obtain further information about Windows network messages.   |
| `Net Localgroup` | Add, modify, delete, or display local group account information in the local or domain directory database. |
| `Net Name`       | Add, delete, or display the names or aliases that the Messenger service recognizes as representing your computer. |
| `Net Pause`      | Pause a Windows service to allow users to disconnect before stopping it. |
| `Net Print`      | Display and manage jobs in a print queue.                    |
| `Net Send`       | Send a message to a user or computer over the network.       |
| `Net Session`    | Display the list of currently connected sessions on the local computer. |
| `Net Share`      | Create, delete, or display shared resources.                 |
| `Net Start`      | Display a list of running services or start a specific stopped service. |
| `Net Statistics` | Display statistics about the Server and Workstation services. |
| `Net Stop`       | Stop a specified Windows service that is currently running.  |
| `Net Time`       | Synchronize the computer’s clock with that of another computer or domain, or display the time for a computer or domain. |
| `Net Use`        | Connect or disconnect to shared resources or display information about connections. |
| `Net User`       | Add, modify, delete, or display user account information in the local or domain directory database. |
| `Net View`       | Display a list of computers in the domain or display the shared resources available on a specific computer. |

| **Command**    | **Description**                                              |
| -------------- | ------------------------------------------------------------ |
| `Net Config`   | Display current computer settings.                           |
| `Net Diag`     | Run the Microsoft Network Diagnostic program to display diagnostic information about a computer. |
| `Net Help`     | Obtain a list of net commands or get help for a specific net command or error message. |
| `Net Init`     | Load protocol and network-adapter drivers without binding them to Protocol Manager. |
| `Net Logoff`   | Break connections to network resources.                      |
| `Net Logon`    | Log on to a domain.                                          |
| `Net Password` | Change logon password.                                       |
| `Net Print`    | Display and manage jobs in a print queue.                    |
| `Net Start`    | Start services.                                              |
| `Net Stop`     | Stop services.                                               |
| `Net Time`     | Synchronize the computer’s clock with that of another computer or workgroup, or display the time for a computer or workgroup. |
| `Net Use`      | Connect or disconnect to shared resources or display information about connections. |
| `Net Ver`      | Display information about workgroup redirector.              |
| `Net View`     | Display a list of computers in the workgroup or display the shared resources available on a specific computer. |

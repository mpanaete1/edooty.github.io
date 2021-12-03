<h1>Introduction to Windows</h1>

[Home](index.html)

[toc]

| Windows Versions | Windows Server Version        |
| ---------------- | ----------------------------- |
| Windows 1        | Windows Server 2003           |
| Windows 2        | Windows Server 2008           |
| Windows 2.x      | Windows Server 2012 / 2012 R2 |
| Windows 3.x      | Windows Server 2016           |
| Windows 95       | Windows Server 2019           |
| Windows 98       |                               |
| Windows NT       |                               |
| Windows XP       |                               |
| Windows Vista    |                               |
| Windows 7        |                               |
| Windows 8.x      |                               |
| Windows 10       |                               |
| Windows 11       |                               |

### Windows File System and Permissions

[Top](windows.html)

The method of keeping track of files on a disk or partition

Windows file system structure

- ​	Logical drives (C:\)
- ​	Folders (default- Documents, Downloads)
- ​	Files

| Folders on C drive    | Roles                                                        |
| --------------------- | ------------------------------------------------------------ |
| PerfLogs              | stores the system issues and other reports regarding performance |
| Program files + (x86) | Programs install default location                            |
| Users                 | Users stored data. Stores users generated data. Saving a file on your desktop |
| Windows               | contains the code to run the OS and some utility tools       |

**Permissions**

File permissions can be set by an administrator or a privileged account. permissions can be applied to Users and Groups

| Permission           | Access                                                       |
| -------------------- | ------------------------------------------------------------ |
| Full control         | allows the user(s)/group(s) to set the ownership of the folder, set permission for others, modify, read, write, and execute files |
| Modify               | allows the user(s)/group(s) to modify, read, write, and execute files. |
| Read & Execute       | allows the user(s)/group(s) to read and execute files.       |
| List folders content | allows the user(s)/group(s) to list the contents (files, subfolders, etc) of a folder. |
| Read                 | only allows the user(s)/group(s) to read files               |
| Write                | allows the user(s)/group(s) to write data to the specified folder (automatically set when "Modify" right is checked) |

Set permissions by right clicking on a file/folder and select `properties` and go to the `security` tab and `edit` when complete click `apply`



You can use the tool `icacls` to check files/folder permissions 

Use `icacls` on its own to get help

Set permissions `icacls <folder/file> /setowner Users` 



### Understanding the authentication Process

[Top](windows.html)

### Utility Tools

[Top](windows.html)

### Types of Servers

[Top](windows.html)

### Users and Group Management

[Top](windows.html)

### Creating your first Group Policy Objects (GPO)

[Top](windows.html)
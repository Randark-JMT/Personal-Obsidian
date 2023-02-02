> https://tryhackme.com/room/blue
> #Offensive #Practice 

# Task 1 Recon

介绍了此环节的内容
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap --script=vuln 10.10.194.231
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-02 14:02 CST
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.10.194.231
Host is up (0.33s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49158/tcp open  unknown
49160/tcp open  unknown

Host script results:
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED

Nmap done: 1 IP address (1 host up) scanned in 132.00 seconds

```
![[Pasted image 20230102140602.png]]

# Task 2 Gain Access

msf直接无脑一把梭就好了

```shell
meterpreter > ps

Process List
============

 PID   PPID  Name                  Arch  Session  User                          Path
 ---   ----  ----                  ----  -------  ----                          ----
 0     0     [System Process]
 4     0     System                x64   0
 416   4     smss.exe              x64   0        NT AUTHORITY\SYSTEM           \SystemRoot\System32\smss.exe
 444   656   LogonUI.exe           x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\LogonUI.exe
 464   704   svchost.exe           x64   0        NT AUTHORITY\SYSTEM
 556   548   csrss.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 604   548   wininit.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\wininit.exe
 616   596   csrss.exe             x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 656   596   winlogon.exe          x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\winlogon.exe
 692   704   svchost.exe           x64   0        NT AUTHORITY\SYSTEM
 704   604   services.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\services.exe
 712   604   lsass.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsass.exe
 720   604   lsm.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsm.exe
 828   704   svchost.exe           x64   0        NT AUTHORITY\SYSTEM
 860   692   taskeng.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\taskeng.exe
 896   704   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE
 916   692   WMIADAP.exe           x64   0        NT AUTHORITY\SYSTEM           \\?\C:\Windows\system32\wbem\WMIADAP.EXE
 944   704   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE
 1072  704   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE
 1176  704   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE
 1308  704   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 1344  704   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE
 1404  704   amazon-ssm-agent.exe  x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\SSM\amazon-ssm-agent.exe
 1480  704   LiteAgent.exe         x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\XenTools\LiteAgent.exe
 1616  704   Ec2Config.exe         x64   0        NT AUTHORITY\SYSTEM           C:\Program Files\Amazon\Ec2ConfigService\Ec2Config.exe
 1668  704   TrustedInstaller.exe  x64   0        NT AUTHORITY\SYSTEM
 1944  704   svchost.exe           x64   0        NT AUTHORITY\NETWORK SERVICE
 2044  828   WmiPrvSE.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\wbem\wmiprvse.exe
 2104  704   mscorsvw.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\Microsoft.NET\Framework64\v4.0.30319\mscorsvw.exe
 2112  828   WmiPrvSE.exe
 2256  2284  mscorsvw.exe          x86   0        NT AUTHORITY\SYSTEM           C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscorsvw.exe
 2284  704   mscorsvw.exe          x86   0        NT AUTHORITY\SYSTEM           C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscorsvw.exe
 2404  704   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE
 2456  704   sppsvc.exe            x64   0        NT AUTHORITY\NETWORK SERVICE
 2584  704   svchost.exe           x64   0        NT AUTHORITY\SYSTEM
 2616  704   vds.exe               x64   0        NT AUTHORITY\SYSTEM
 2764  704   SearchIndexer.exe     x64   0        NT AUTHORITY\SYSTEM
 2812  556   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe
 2908  2728  powershell.exe        x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe

```

# Task 3 Escalate

将meterpreter所在的进程进行转移就好

# Task 4 Cracking

执行一遍`hashdump`，然后查彩虹表即可

# Task 5 Find flags!

在关键位置找flag即可
```plaintext
c:/
c:/windows/system32/config/
c:/users/jon/documents/
```
![[Pasted image 20230102143555.png]]
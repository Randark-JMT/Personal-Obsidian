> https://tryhackme.com/room/introtoshells
> #Offensive #GrantPrivilege 

# Task 1 What is a shell?

介绍了何为shell

# Task 2 Tools

介绍了使用**Netcat**，**Socat**，**Metasploit -- multi/handler**和**Msfvenom**处理远程shell
并介绍了一些储存shell payload 的储存库：[Payloads all the Things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md).，[Reverse Shell Cheatsheet](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) 和 [SecLists repo](https://github.com/danielmiessler/SecLists)

# Task 3 Types of Shell

介绍了shell的种类：反向shell-正向shell，交互式shell与非交互式shell
![[Pasted image 20230110143914.png]]

# Task 4 Netcat

介绍了使用Netcat进行shell相关操作

# Task 5 Netcat Shell Stabilisation

介绍了如何使用 _Python_ / _rlwrap_ / _Socat_ 来获得一个更加稳定的、具有交互性的shell。同时也介绍了使用`stty`对shell的外观进行调整

# Task 6 Socat

介绍了如何使用`socat`建立shell连接

# Task 7 Socat Encrypted Shells

介绍了如何创建加密的shell连接
![[Pasted image 20230112145115.png]]

# Task 8 Common Shell Payloads

介绍了如何生成shell的payload

# Task 9 msfvenom

介绍了使用msf框架进行shell的构建，以及如何使用msfvenom自动化生成攻击载荷
![[Pasted image 20230113120329.png]]

# Task 10 Metasploit multi/handler

介绍了如何使用msfconsole进行侦听shell

# Task 11 WebShells

介绍了webhsell，以及kali自带的一些webshell

# Task 12 Next Steps

介绍在拿到临时shell之后，如何获得一个更加稳定的shell（如ssh，或者rdp）

# Task 13 Practice and Examples

练习

# Task 14 Linux Practice Box

提供了一台远程Linux靶机

# Task 15 Windows Practice Box

提供了一台Windows靶机
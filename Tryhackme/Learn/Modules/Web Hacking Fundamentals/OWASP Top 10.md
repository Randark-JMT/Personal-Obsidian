> https://tryhackme.com/room/owasptop10
> #Offensive 

# Task 1 Introduction

介绍了OWASP中常见的漏洞：
-   Injection
-   Broken Authentication
-   Sensitive Data Exposure
-   XML External Entity
-   Broken Access Control
-   Security Misconfiguration
-   Cross-site Scripting
-   **I**nsecure Deserialization
-   Components with Known Vulnerabilities
-   Insufficent Logging & Monitoring

# Task 2 Accessing machines

介绍了如何连接到Tryhackme的靶机网络

# Task 3 [Severity 1] Injection

介绍了何为注入攻击：SQL注入攻击和命令注入攻击

# Task 4 [Severity 1] OS Command Injection

介绍了命令注入

# Task 5 [Severity 1] Command Injection Practical

提供了一个模拟的webshell，来展示命令注入攻击

```shell
ls
css drpepper.txt evilshell.php index.php js 

cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing
List
Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats
Bug-Reporting
System
(admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd
Network
Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd
Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin

id
uid=33(www-data) gid=33(www-data) groups=33(www-data) 

lsb_release -a 
Distributor ID: Ubuntu Description: Ubuntu 18.04.4 LTS Release: 18.04 Codename: bionic 

cat /etc/update-motd.d/00-header 
#!/bin/sh # # 00-header - create the header of the MOTD 
# Copyright (C) 2009-2010 Canonical Ltd. 
# 
# Authors: Dustin Kirkland 
# 
# This program is free software; you can redistribute it and/or modify 
# it under the terms of the GNU General Public License as published by 
# the Free Software Foundation; either version 2 of the License, or 
# (at your option) any later version. 
# 
# This program is distributed in the hope that it will be useful, 
# but WITHOUT ANY WARRANTY; without even the implied warranty of 
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the 
# GNU General Public License for more details. 
# 
# You should have received a copy of the GNU General Public License along 
# with this program; if not, write to the Free Software Foundation, Inc., 
# 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA. 
[ -r /etc/lsb-release ] && . /etc/lsb-release if [ -z "$DISTRIB_DESCRIPTION" ] && [ -x /usr/bin/lsb_release ]; then 
# Fall back to using the very slow lsb_release utility 
DISTRIB_DESCRIPTION=$(lsb_release -s -d) fi printf "Welcome to %s (%s %s %s)\n" "$DISTRIB_DESCRIPTION" "$(uname -o)" "$(uname -r)" "$(uname -m)" DR PEPPER MAKES THE WORLD TASTE BETTER! 
```
![[Pasted image 20230118101202.png]]

# Task 6 [Severity 2] Broken Authentication

介绍了在身份验证和会话管理这块，可能存在的漏洞，以及常见的攻击手法

# Task 7 [Severity 2] Broken Authentication Practical

提供了一台靶机，介绍了一些身份验证漏洞
![[Pasted image 20230118102047.png]]

# Task 8 [Severity 3] Sensitive Data Exposure (Introduction)

介绍了何为“敏感数据泄露”漏洞

# Task 9 [Severity 3] Sensitive Data Exposure (Supporting Material 1)

介绍了SQLite数据库

# Task 10 [Severity 3] Sensitive Data Exposure (Supporting Material 2)

介绍了如何通过查彩虹表的形式逆向还原哈希

# Task 11 [Severity 3] Sensitive Data Exposure (Challenge)

给出了一个模拟网站，相对简单
操作SQLite数据库的时候，用一些工具（如DBeaver）会更方便
![[Pasted image 20230118103238.png]]

# Task 12 [Severity 4] XML External Entity

介绍了XXE攻击

# Task 13 [Severity 4 XML External Entity - eXtensible Markup Language

介绍了XML文档的标准以及格式

# Task 14 [Severity 4] XML External Entity - DTD

介绍了XML的文档类型定义（DTD）
![[Pasted image 20230120204117.png]]

Task 15 [Severity 4] XML External Entity - XXE Payload

Task 16 [Severity 4] XML External Entity - Exploiting

Task 17 [Severity 5] Broken Access Control

Task 18 [Severity 5] Broken Access Control (IDOR Challenge)

Task 19 [Severity 6] Security Misconfiguration

Task 20 [Severity 7] Cross-site Scripting

Task 21 [Severity 8] Insecure Deserialization

Task 22 [Severity 8] Insecure Deserialization - Objects

Task 23 [Severity 8] Insecure Deserialization - Deserialization

Task 24 [Severity 8] Insecure Deserialization - Cookies

Task 25 [Severity 8] Insecure Deserialization - Cookies Practical

Task 26 [Severity 8] Insecure Deserialization - Code Execution

Task 27 [Severity 9] Components With Known Vulnerabilities - Intro

Task 28 [Severity 9] Components With Known Vulnerabilities - Exploit

Task 29 [Severity 9] Components With Known Vulnerabilities - Lab

Task 30 [Severity 10] Insufficient Logging and Monitoring

Task 31 What Next?
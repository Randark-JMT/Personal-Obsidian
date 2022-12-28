> https://tryhackme.com/room/nmap02
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍，本节主要介绍端口扫描
![[Pasted image 20221228113419.png]]

# Task 2 TCP and UDP Ports

介绍了TCP和UDP的端口状态

# Task 3 TCP Flags

介绍了`TCP`协议传输数据的数据结构
![[Pasted image 20221228114613.png]]

# Task 4 TCP Connect Scan

介绍了利用`nmap`进行端口连续扫描
使用`nmap -sT TARGETS`进行基于`TCP`的连续端口扫描
```shell
┌──(randark㉿kali)-[~]
└─$ nmap -sT 10.10.13.101
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-28 13:01 CST
Nmap scan report for 10.10.13.101
Host is up (0.24s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT    STATE SERVICE
22/tcp  open  ssh
25/tcp  open  smtp
80/tcp  open  http
110/tcp open  pop3
111/tcp open  rpcbind
143/tcp open  imap

Nmap done: 1 IP address (1 host up) scanned in 27.20 seconds
```

# Task 5 TCP SYN Scan

介绍了利用`nmap`进行`TCP SYN`扫描
使用`nmap -sS TARGETS`进行基于`TCP SYN`的扫描，此举可以减少扫描被记录的概率
```shell
┌──(root㉿kali)-[/home/randark]
└─# nmap -sS 10.10.188.59
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-28 13:09 CST
Nmap scan report for 10.10.188.59
Host is up (0.25s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
80/tcp   open  http
110/tcp  open  pop3
111/tcp  open  rpcbind
143/tcp  open  imap
6667/tcp open  irc

Nmap done: 1 IP address (1 host up) scanned in 8.31 seconds
```

# Task 6 UDP Scan

介绍了利用`nmap`进行`UDP`扫描
使用`nmap -sU TARGETS`进行基于`UDP`的扫描
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -sU -F -v 10.10.38.216
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-28 22:17 CST
UDP Scan Timing: About 42.30% done; ETC: 22:19 (0:00:42 remaining)
Completed UDP Scan at 22:19, 104.84s elapsed (100 total ports)
Nmap scan report for 10.10.38.216
Host is up (0.30s latency).
Not shown: 97 closed udp ports (port-unreach)
PORT    STATE         SERVICE
53/udp  open|filtered domain
68/udp  open|filtered dhcpc
111/udp open          rpcbind

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 105.42 seconds
           Raw packets sent: 290 (16.543KB) | Rcvd: 107 (8.762KB)
```

# Task 7 Fine-Tuning Scope and Performance

介绍了如何利用参数，对`namp`的扫描行为进行微调和优化
- `-T`参数，可以调整扫描时间
- `-p`，控制扫描的端口范围
- `-min-rate`，`--max-rate`，控制数据包的速率
- `--min-parallelism`，`--max-parallelism`，控制并行扫描设备的数量

# Task 8 Summary

总结
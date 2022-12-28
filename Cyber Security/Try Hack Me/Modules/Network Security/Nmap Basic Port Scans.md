> https://tryhackme.com/room/nmap02
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍，本节主要介绍端口扫描
![[Pasted image 20221228113419.png]]

# Task 2 TCP and UDP Ports

介绍了`TCP`协议传输数据的数据结构
![[Pasted image 20221228114613.png]]

# Task 3 TCP Flags

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

# Task 4 TCP Connect Scan

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

# Task 5 TCP SYN Scan

介绍了利用`nmap`进行`UDP`扫描
使用`nmap -sU TARGETS`进行基于`UDP`的扫描
```shell

```

Task 6 UDP Scan

Task 7 Fine-Tuning Scope and Performance

Task 8 Summary
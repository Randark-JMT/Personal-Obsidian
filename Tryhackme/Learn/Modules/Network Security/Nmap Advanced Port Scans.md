> https://tryhackme.com/room/nmap03
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍，介绍了一些更为高级的扫描手法

# Task 2 TCP Null Scan, FIN Scan, and Xmas Scan

介绍了三种类别的扫描手法：
-   Null Scan，`-sN`
-   FIN Scan，`-sF`
-   Xmas Scan，`-sX`

对靶机进行`FIN scan`：
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -sF 10.10.11.96       
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-29 09:53 CST
Nmap scan report for 10.10.11.96
Host is up (0.32s latency).
Not shown: 993 closed tcp ports (reset)
PORT    STATE         SERVICE
22/tcp  open|filtered ssh
25/tcp  open|filtered smtp
53/tcp  open|filtered domain
80/tcp  open|filtered http
110/tcp open|filtered pop3
111/tcp open|filtered rpcbind
143/tcp open|filtered imap

Nmap done: 1 IP address (1 host up) scanned in 10.70 seconds
```

靶机进行`null scan`：
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -sN 10.10.11.96
Starting Nmap 7.93 ( https://nmap.org ) at 2022-12-29 09:54 CST
Nmap scan report for 10.10.11.96
Host is up (0.32s latency).
Not shown: 993 closed tcp ports (reset)
PORT    STATE         SERVICE
22/tcp  open|filtered ssh
25/tcp  open|filtered smtp
53/tcp  open|filtered domain
80/tcp  open|filtered http
110/tcp open|filtered pop3
111/tcp open|filtered rpcbind
143/tcp open|filtered imap

Nmap done: 1 IP address (1 host up) scanned in 9.21 seconds
```

# Task 3 TCP Maimon Scan

介绍了如何使用`nmap`进行`TCP Maimon`扫描

# Task 4 TCP ACK, Window, and Custom Scan

介绍了如何进行基于`TCP ACK`的扫描、`TCP window`扫描，以及自定义的扫描
![[Pasted image 20230102145915.png]]

# Task 5 Spoofing and Decoys

介绍了如何进行带有欺骗性的扫描，使得目标的响应数据包发往其他地址，从而隐藏攻击者的行为
![[Pasted image 20230106202748.png]]

# Task 6 Fragmented Packets

介绍了如何指定将数据包进行分片，从而绕过IDS的监控

# Task 7 Idle/Zombie Scan

欺骗性扫描具有一定的局限性，因为欺骗性扫描要求攻击者能够监控区域内的网络流量，才能分析出来目标机器的具体响应。然后通过僵尸机，nmap同样能进行类似于欺骗性扫描的扫描行动，这被称之为僵尸扫描（空闲扫描）

# Task 8 Getting More Details

介绍了如何使nmap的输出信息中添加更多细节，如扫描过程，以及为何判断相关数据（如是如何判断端口的打开情况）

# Task 9 Summary

总结
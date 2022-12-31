> https://tryhackme.com/room/nmap03
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍，介绍了一些更为高级的扫描手法

# Task 2 TCP Null Scan, FIN Scan, and Xmas Scan

<<<<<<< HEAD
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

=======
pass
>>>>>>> origin/main


Task 4 TCP ACK, Window, and Custom Scan

Task 5 Spoofing and Decoys

Task 6 Fragmented Packets

Task 7 Idle/Zombie Scan

Task 8 Getting More Details

Task 9 Summary
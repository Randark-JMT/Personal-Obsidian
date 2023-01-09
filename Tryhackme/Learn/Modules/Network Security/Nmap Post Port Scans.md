> https://tryhackme.com/room/nmap04
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍

# Task 2 Service Detection

介绍了如何进行服务探测
```shell
┌──(randark㉿kali)-[~]
└─$ sudo nmap -sV --version-light 10.10.157.46
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-07 09:10 CST
Nmap scan report for 10.10.157.46
Host is up (0.24s latency).
Not shown: 994 closed tcp ports (reset)
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
25/tcp  open  smtp    Postfix smtpd
80/tcp  open  http    nginx 1.6.2
110/tcp open  pop3    Dovecot pop3d
111/tcp open  rpcbind
143/tcp open  imap    Dovecot imapd
Service Info: Host:  debra2.thm.local; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.45 seconds
```
![[Pasted image 20230107091342.png]]

# Task 3 OS Detection and Traceroute

介绍了如何对目标的系统进行探测，并介绍了如何追踪与目标之间的路由

> 这一步没办法复现，因为由于openvpn的缘故，相关指纹信息好像传输发生了改变

# Task 4 Nmap Scripting Engine (NSE)

介绍了如何使用nmap内置的脚本增强其扫描
```shell
┌──(randark㉿kali)-[/usr/share/nmap/scripts]
└─$ sudo nmap -sS -sC 10.10.199.104
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-07 09:24 CST
Nmap scan report for 10.10.199.104
Host is up (0.23s latency).
Not shown: 993 closed tcp ports (reset)
PORT    STATE SERVICE
22/tcp  open  ssh
| ssh-hostkey: 
|   1024 d58097a3a83b57782f0a78aead3424f4 (DSA)
|   2048 aa667a45ebd18c00e31231d8768eed3a (RSA)
|   256 3d8272a307492ecbd987db08c6905665 (ECDSA)
|_  256 dcf00c89708765ba52b1e959f75dd26a (ED25519)
25/tcp  open  smtp
| ssl-cert: Subject: commonName=debra2.thm.local
| Not valid before: 2021-08-10T12:10:58
|_Not valid after:  2031-08-08T12:10:58
|_smtp-commands: debra2.thm.local, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
|_ssl-date: TLS randomness does not represent time
53/tcp  open  domain
| dns-nsid: 
|_  bind.version: 9.9.5-9+deb8u19-Debian
80/tcp  open  http
|_http-title: Welcome to nginx on Debian!
110/tcp open  pop3
|_pop3-capabilities: RESP-CODES AUTH-RESP-CODE UIDL PIPELINING SASL CAPA TOP
111/tcp open  rpcbind
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          47773/udp   status
|   100024  1          49144/tcp   status
|   100024  1          50089/udp6  status
|_  100024  1          56879/tcp6  status
143/tcp open  imap
|_imap-capabilities: ENABLE SASL-IR more capabilities LITERAL+ OK have ID LOGIN-REFERRALS Pre-login listed LOGINDISABLEDA0001 IDLE post-login IMAP4rev1

Nmap done: 1 IP address (1 host up) scanned in 30.10 seconds

┌──(randark㉿kali)-[/usr/share/nmap/scripts]
└─$ sudo nmap -sS --script=ssh2-enum-algos 10.10.199.104
Starting Nmap 7.93 ( https://nmap.org ) at 2023-01-07 09:26 CST
Nmap scan report for 10.10.199.104
Host is up (0.23s latency).
Not shown: 993 closed tcp ports (reset)
PORT    STATE SERVICE
22/tcp  open  ssh
| ssh2-enum-algos: 
|   kex_algorithms: (6)
|       curve25519-sha256@libssh.org
|       ecdh-sha2-nistp256
|       ecdh-sha2-nistp384
|       ecdh-sha2-nistp521
|       diffie-hellman-group-exchange-sha256
|       diffie-hellman-group14-sha1
|   server_host_key_algorithms: (4)
|       ssh-rsa
|       ssh-dss
|       ecdsa-sha2-nistp256
|       ssh-ed25519
|   encryption_algorithms: (6)
|       aes128-ctr
|       aes192-ctr
|       aes256-ctr
|       aes128-gcm@openssh.com
|       aes256-gcm@openssh.com
|       chacha20-poly1305@openssh.com
|   mac_algorithms: (10)
|       umac-64-etm@openssh.com
|       umac-128-etm@openssh.com
|       hmac-sha2-256-etm@openssh.com
|       hmac-sha2-512-etm@openssh.com
|       hmac-sha1-etm@openssh.com
|       umac-64@openssh.com
|       umac-128@openssh.com
|       hmac-sha2-256
|       hmac-sha2-512
|       hmac-sha1
|   compression_algorithms: (2)
|       none
|_      zlib@openssh.com
25/tcp  open  smtp
53/tcp  open  domain
80/tcp  open  http
110/tcp open  pop3
111/tcp open  rpcbind
143/tcp open  imap

Nmap done: 1 IP address (1 host up) scanned in 3.73 seconds
```

# Task 5 Saving the Output

介绍了nmap如何保存扫描结果
```shell
┌──(randark㉿kali)-[~]
└─$ grep https scan_172_17_network.gnmap 
Host: 172.17.0.215 ()   Ports: 22/closed/tcp//ssh///, 80/open/tcp//http///, 443/open/tcp//https///      Ignored State: filtered (997)
Host: 172.17.19.249 ()  Ports: 22/open/tcp//ssh///, 53/open/tcp//domain///, 80/open/tcp//http///, 443/open/tcp//https///        Ignored State: closed (996)
Host: 172.17.23.240 ()  Ports: 22/closed/tcp//ssh///, 80/open/tcp//http///, 443/open/tcp//https///      Ignored State: filtered (997)
                                                                                                                                                                                                                                           
┌──(randark㉿kali)-[~]
└─$ grep 8089 scan_172_17_network.gnmap 
Host: 172.17.20.147 ()  Ports: 22/open/tcp//ssh///, 8000/open/tcp//http-alt///, 8089/open/tcp//unknown///       Ignored State: closed (997)
```

# Task 6 Summary

总结
> https://tryhackme.com/room/activerecon
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍-何为主动侦查

# Task 2 Web Browser

介绍了浏览器插件和开发者工具
![[Pasted image 20221224101701.png]]

# Task 3 Ping

介绍了如何使用`ping`
![[Pasted image 20221224102144.png]]

# Task 4 Traceroute

介绍了使用`traceroute`进行路由跟踪
![[Pasted image 20221224115218.png]]

# Task 5 Telnet

介绍了使用`telnat`与远程服务器进行交互
```shell
┌──(randark㉿kali)-[~]
└─$ telnet 10.10.83.23 80 
Trying 10.10.83.23...
Connected to 10.10.83.23.
Escape character is '^]'.
GET / HTTP/1.1
host:telnet

HTTP/1.1 200 OK
Date: Sat, 24 Dec 2022 03:49:35 GMT
Server: Apache/2.4.10 (Debian)
Last-Modified: Mon, 30 Aug 2021 12:09:24 GMT
ETag: "15-5cac5b436ddfa"
Accept-Ranges: bytes
Content-Length: 21
Content-Type: text/html
```
![[Pasted image 20221224115126.png]]

# Task 6 Netcat

介绍了网络的瑞士军刀 - Netcat的使用
![[Pasted image 20221224205156.png]]

# Task 7 Putting It All Together

总结
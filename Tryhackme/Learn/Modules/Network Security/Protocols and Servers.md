> https://tryhackme.com/room/protocolsandservers
> #Network-Structure 

# Task 1 Introduction

前置介绍

# Task 2 Telnet

介绍了telnet协议

# Task 3 Hypertext Transfer Protocol (HTTP)

介绍了http协议
```shell
┌──(randark㉿kali)-[~]
└─$ telnet 10.10.58.163 80
Trying 10.10.58.163...
Connected to 10.10.58.163.
Escape character is '^]'.
GET /flag.thm HTTP/1.1
host: telnet

HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Sat, 07 Jan 2023 01:51:43 GMT
Content-Type: application/octet-stream
Content-Length: 39
Last-Modified: Wed, 15 Sep 2021 09:19:23 GMT
Connection: keep-alive
ETag: "6141ba9b-27"
Accept-Ranges: bytes

THM{e3eb0a1df437f3f97a64aca5952c8ea0}
```

# Task 4 File Transfer Protocol (FTP)

介绍了ftp协议

# Task 5 Simple Mail Transfer Protocol (SMTP)

介绍了SMTP协议

# Task 6 Post Office Protocol 3 (POP3)

介绍了POP3协议

# Task 7 Internet Message Access Protocol (IMAP)

介绍了IMAP协议

# Task 8 Summary

总结
> https://tryhackme.com/room/passiverecon
> #Offensive #Reconnaissance

# Task 1 Introduction

前置介绍，如何进行被动网络侦察

# Task 2 Passive Versus Active Recon

介绍了被动与主动侦察之间的差异
![[Pasted image 20221223215904.png]]

# Task 3 Whois

介绍了如何查询whois信息进行被动侦查
![[Pasted image 20221223220441.png]]

# Task 4 nslookup and dig

介绍了如何使用`nslookup`进行网络侦查
```shell
┌──(randark㉿kali)-[~]
└─$ nslookup -type=txt thmlabs.com  
Server:         192.168.23.2
Address:        192.168.23.2#53

Non-authoritative answer:
thmlabs.com     text = "THM{a5b83929888ed36acb0272971e438d78}"
```

# Task 5 DNSDumpster

介绍了使用 [DNSDumpster](https://dnsdumpster.com/) 进行网络侦查
![[Pasted image 20221224093355.png]]
![[Pasted image 20221224093343.png]]

# Task 6 Shodan.io

介绍了利用 Shodan.io 进行网络侦查
![[Pasted image 20221224093813.png]]

# Task 7 Summary


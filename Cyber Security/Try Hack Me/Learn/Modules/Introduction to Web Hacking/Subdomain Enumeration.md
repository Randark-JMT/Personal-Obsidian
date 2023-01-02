> https://tryhackme.com/room/subdomainenumeration
> #Offensive #Web-Hacking #Subdomain

# Task 1 Brief

前置介绍 - 子域枚举
![[Pasted image 20221220131430.png]]

# Task 2 OSINT - SSL/TLS Certificates

介绍了通过SSL证书进行子域枚举，并推荐了：[crt.sh](https://crt.sh)

# Task 3 OSINT - Search Engines

介绍了如何通过Google进行子域枚举
```plaintext
-site:www.tryhackme.com site:*.tryhackme.com
```
![[Pasted image 20221220132042.png]]

# Task 4 DNS Bruteforce

介绍了使用自动化工具爆破子域

# Task 5 OSINT - Sublist3r

介绍了使用自动化工具完成[[#Task 3 OSINT - Search Engines]]中所介绍的，基于搜索引擎的OSINT子域枚举
[aboul3la / Sublist3r](https://github.com/aboul3la/Sublist3r)

# Task 6 Virtual Hosts

介绍了如何使用自动化工具，对虚拟主机进行探测
```shell
# Example
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.211.0
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.211.0 -fs {size}
```
![[Pasted image 20221220140255.png]]
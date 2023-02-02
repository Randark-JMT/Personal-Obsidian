> https://tryhackme.com/room/contentdiscovery
> Writeup：[Content Discovery TryHackme](https://infosecwriteups.com/content-discovery-tryhackme-3254015ccd11)
> #Offensive #Web-Hacking

# Task 1 What Is Content Discovery?

前置介绍

# Task 2 Manual Discovery - Robots.txt

简单，介绍了`robots.txt`

# Task 3 Manual Discovery - Favicon

这个比较实用，通过框架的图标来识别框架
```shell
# 获取框架icon的哈希
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
# 而后和数据库中的样本进行对比
https://wiki.owasp.org/index.php/OWASP_favicon_database
```

# Task 4 Manual Discovery - Sitemap.xml

介绍了如何通过`Sitemap.xml`探测网站结构

# Task 5 Manual Discovery - HTTP Headers

介绍了如何使用`curl <url> -v`来查看网站http响应的HTTP头

# Task 6 Manual Discovery - Framework Stack

介绍了通过网站框架的信息来探测网站的敏感页面（如后台）

# Task 7 OSINT - Google Hacking / Dorking

介绍了通过搜索引擎收集开源网络情报（如Google）

# Task 8 OSINT - Wappalyzer

介绍了`Wappalyzer`

# Task 9 OSINT - Wayback Machine

介绍了[Wayback Machine](https://archive.org/web/)

# Task 10 OSINT - GitHub

介绍了[Github](https://github.com)

# Task 11 OSINT - S3 Buckets

介绍了由Amazon AWS提供的S3 Buckets服务

# Task 12 Automated Discovery

介绍了自动化扫描探测的工具：`ffuf`，`dirb`和`gobuster`

> 这一节要求使用他们所提供的字典

```shell
# Example
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://10.10.74.192/FUZZ
dirb http://10.10.74.192/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
gobuster dir --url http://10.10.74.192/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```
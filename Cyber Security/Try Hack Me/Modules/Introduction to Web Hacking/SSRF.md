> https://tryhackme.com/room/ssrfqi
> #Offensive #Web-Hacking #SSRF

# Task 1 What is an SSRF?

前置介绍i，介绍了什么是SSRF
![[Pasted image 20221221194217.png]]

# Task 2 SSRF Examples

一个简单的小实例，最后的链接为：`https://website.thm/item/9?server=server.website.thm/flag?id=9&x=`

# Task 3 Finding an SSRF

介绍了如何寻找一个可能的SSRF漏洞，并推荐了[requestbin.com](https://requestbin.com)

# Task 4 Defeating Common SSRF Defenses

介绍了一些绕过方法
![[Pasted image 20221221203548.png]]

# Task 5 SSRF Practical

一个针对SSRF的一个小示例，手把手教你完成一个简单的SSRF利用
```shell
/private --> x/../private
```
通过加入`../`，实现目录穿越，从而实现对敏感目录中数据的读取
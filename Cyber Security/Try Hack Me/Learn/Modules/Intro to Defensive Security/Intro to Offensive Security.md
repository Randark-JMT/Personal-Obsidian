> https://tryhackme.com/room/introtooffensivesecurity
> #Basic #Offensive
>作为安全研究的入门，基本就是手把手教你了，好良心🥰

# Task 1 Hacking your first machine
基本就是依靠目录爆破来完成的，其核心就是通过扫描器扫描到后台的转账后台页面，然后给自己转账
~~*现实作战的时候真的不怕查到自己头上吗*~~
第一步就是目录扫描
```shell
gobuster -u http://fakebank.com -w wordlist.txt dir  
```
成功扫描出`/bank-transfer`这个路由之后，直接访问，并从`2276`这个账户给自己的账户`8881`转账2000刀之后，任务就完成了。最终账户余额页面就会显示 flag：`BAND-HACKED`
![[Pasted image 20221215101959.png]]

# Task 2 What is Offensive Security?

看文章就行了

# Task 3 Careers in cyber security

同上
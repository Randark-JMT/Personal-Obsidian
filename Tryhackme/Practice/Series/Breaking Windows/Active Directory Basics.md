> https://tryhackme.com/room/activedirectorybasics
> #Offensive #Active-Directory

# Task 1 Introduction

前置介绍，何为AD域，以及其作用

# Task 2 Physical Active Directory

介绍了AD域的物理组成
![[Pasted image 20230106104058.png]]

# Task 3 The Forest

介绍了AD域中Tree与Forests的概念
![[Pasted image 20230106104131.png]]

# Task 4 Users + Groups

介绍了AD域中用户与用户组的概念
![[Pasted image 20230106104159.png]]

# Task 5 Trusts + Policies

介绍了域之间信任与策略的传递
![[Pasted image 20230106195328.png]]

# Task 6 Active Directory Domain Services + Authentication

介绍了在AD域会提供的域服务以及身份验证服务
![[Pasted image 20230106195640.png]]

# Task 7 AD in the Cloud

介绍了云上的AD服务
![[Pasted image 20230106195915.png]]

# Task 8 Hands-On Lab

提供了一台远程的AD域控制器作为靶机，用于演示基本的AD域操作实验
```powershell
Get-NetComputer -fulldata | select operatingsystem
Get-NetUser | select cn
```
![[Pasted image 20230106201725.png]]

# Task 9 Conclusion

总结
> https://tryhackme.com/room/burpsuiteintruder
> #Burp-Suite #Offensive 
# Task 1 Introduction Room Outline

前置介绍

# Task 2 Intruder What is Intruder?

介绍了Intruder，以及基础的模块和界面
![[Pasted image 20221216111648.png]]

# Task 3 Intruder Positions

简单介绍了如何控制Positions的设置

# Task 4 Attack Types Introduction

介绍了四大攻击模式

# Task 5 Attack Types Sniper

介绍了`Sniper`这一攻击模式，本质就为在负载集中取出一个负载，放在第一个负载尾，然后类推，依次填充
第一空注意是Sniper模式下进行攻击，所以总共是100*3个请求
![[Pasted image 20221216113551.png]]

# Task 6 Attack Types Battering Ram

介绍了`Battering Ram`这一攻击模式，本质上为在负载集中取出一个负载，填充进所有的负载位
![[Pasted image 20221216113913.png]]

# Task 7 Attack Types Pitchfork

介绍了`Pitchfork`这一攻击模式，本质上为有几个负载位就有几个负载集，依次从中取出一组负载，然后填充进负载位
同时，在多负载集的情况下，最多的请求次数受到最少的负载集的影响
![[Pasted image 20221216114242.png]]

# Task 8 Attack Types Cluster Bomb

介绍了`Cluster Bomb`这一攻击模式，可以视作`Pitchfork`的增强版，其最多的请求次数不会受到最少的负载集的影响
![[Pasted image 20221216115124.png]]

# Task 9 Intruder Payloads

介绍了如何加载并处理载荷
![[Pasted image 20221216115423.png]]

# Task 10 Practical Example

模拟了一个攻击场景

# Task 11 Practical Challenge

![[Pasted image 20221216120625.png]]
![[Pasted image 20221216120629.png]]
![[Pasted image 20221216120614.png]]

![[Pasted image 20221216120645.png]]

# Task 12 Extra Mile CSRF Token Bypass

介绍了如何应对更高级的反制措施并绕过（使用宏）
![[Pasted image 20221216121038.png]]


# Task 13 Conclusion Conclusion

总结
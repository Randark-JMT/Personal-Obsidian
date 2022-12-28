> https://tryhackme.com/room/nmap01
> #Offensive #Reconnaissance 

# Task 1 Introduction

前置介绍

# Task 2 Subnetworks

介绍了主机与子网的概念，并提供了一个在线的模拟器

# Task 3 Enumerating Targets

介绍了如何使用nmap进行目标枚举
```shell
nmap -sL -n 10.10.12.13/29
nmap -sL -n 10.10.0-255.101-125
```
![[Pasted image 20221225140128.png]]

# Task 4 Discovering Live Hosts

介绍了如何搜寻存活的主机
![[Pasted image 20221225140729.png]]

# Task 5 Nmap Host Discovery Using ARP

介绍了通过`ARP`对目标主机进行扫描
> 默认情况下，Nmap 使用 ping 扫描来查找活动主机，然后继续仅扫描活动主机。
> ARP 仅当您与目标系统位于同一子网上时才可以进行 扫描。

- 使用`nmap -PR -sn TARGETS`，通过`ARP`对目标主机进行扫描，`-PR`指定只需要`ARP`扫描
同时介绍了一款针对ARP进行扫描的工具：`arp-scan`，访问 [arp-scan wiki](http://www.royhills.co.uk/wiki/index.php/Main_Page) 获取详细信息

# Task 6 Nmap Host Discovery Using ICMP

介绍了通过`ICMP`对目标主机进行扫描
- 默认使用`nmap -sn TARGETS`，通过`ping`对目标主机进行存活探测，-sn指定不扫描端口
- 使用`nmap -PP -sn MACHINE_IP`，`-PP`指定使用`ICMP时间戳`对目标主机进行探测
- 使用`nmap -PM -sn MACHINE_IP`，`-PM`指定使用`ICMP地址掩码`对目标主机进行探测

# Task 7 Nmap Host Discovery Using TCP and UDP

介绍了基于`TCP`和`UDP`进行主机探测
- 使用`nmap -PS<port> -sn TARGETS`，通过`TCP`对目标主机进行扫描，不指定端口的话默认`80`，`<port>`内多个端口可以用逗号隔开
- 使用`sudo nmap -PA -sn MACHINE_IP`， 通过`TCP ACK`对目标主机进行扫描
- 使用`nmap -PU<port> -sn MACHINE_IP`，通过`UDP`对目标主机进行扫描，存活的主机不会响应，但是离线的主机将会作出`ICMP Type 3，Code 3`的响应

同时介绍了`Masscan`这一工具，可以实现类似的`UDP`扫描
![[Pasted image 20221228110424.png]]

# Task 8 Using Reverse-DNS Lookup

介绍了使用反向DNS对主机名进行搜集

# Task 9 Summary

总结
![[Pasted image 20221228112532.png]]
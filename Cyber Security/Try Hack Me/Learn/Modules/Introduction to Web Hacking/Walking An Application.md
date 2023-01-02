> https://tryhackme.com/room/walkinganapplication
> #Offensive #Web-Hacking 

# Task 1 Walking An Application

介绍了如何在前端对一个网站进行初步检查

# Task 2 Exploring The Website

介绍了目标网站的结构

# Task 3 Viewing The Page Source

介绍了如何从前端数据中分析敏感数据
```url
view-source:http://10-10-165-146.p.thmlabs.com/tmp.zip
view-source:http://10-10-165-146.p.thmlabs.com/secret-page
view-source:http://10-10-165-146.p.thmlabs.com/assets/flag.txt
view-source:http://10-10-165-146.p.thmlabs.com/new-home-beta
```
感觉这块用Burp Suite来处理会更方便
![[Pasted image 20221220102712.png]]

# Task 4 Developer Tools - Inspector

介绍了浏览器的开发者工具中，最常用的模块-检查器
我个人还是更喜欢直接删掉元素节点，但是在css中将可见性改为`none`更优雅就是了。。
![[Pasted image 20221220103827.png]]

# Task 5 Developer Tools - Debugger

介绍了调试器
这个偏简单，下个断点就好
![[Pasted image 20221220104227.png]]

# Task 6 Developer Tools - Network

对我而言第二常用吧，监视网站的流量行为，方便判断网站优化，和看看有无异常信息
![[Pasted image 20221220104916.png]]
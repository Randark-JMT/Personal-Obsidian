> https://tryhackme.com/room/packetsframes
> #Network-Structure 

# Task 1 What are Packets and Frames

简述了数据包（Packet）和帧（Frame）之间的概念
![[Pasted image 20221217141138.png]]

# Task 2 TCP/IP (The Three-Way Handshake)

OSI模型可以看[[OSI Model#^30b0cb|OSI七层模型可视化]]
这一部分主要讲明了TCP数据包的结构（做过`Wireshark`数据分析的人应该比较熟悉），以及TCP三次握手的过程
![[Pasted image 20221217141809.png]]

# Task 3 Practical - Handshake

一个在线可视化，演示了TCP握手的过程
```plaintext
- SYN : Can you hear me Bob?
- SYN/ACK : Yes, I can hear you!
- ACK : Okay Great
--- 三次握手成功，TCP成功建立连接 ---
- DATA : Cheesecake is on sale!
- ACK : I Hear ya!
--- 数据传输完成，开始关闭连接 ---
- FIN/ACK : I'm all done
- FIN/ACK : Yeah Me Too
- ACK : Okay, Goodbye
```
![[Pasted image 20221217142329.png]]

# Task 4 UDP/IP

OSI模型可以看[[OSI Model#^30b0cb|OSI七层模型可视化]]
UDP可以视作TCP的简化版本，最为核心的便是抛弃了数据完整性
![[Pasted image 20221217142732.png]]

# Task 5 Ports 101 (Practical)

简述了端口在进行网络通信时的作用和地位
| **Protocol**                                                       | **Port Number** | **Description** |
| ------------------------------------------------------------------ | --------------- | --------------- |
| **F**ile **T**ransfer **P**rotocol (**FTP**)|          21       |       该协议由基于客户端-服务器模型构建的文件共享应用程序使用，这意味着您可以从中央位置下载文件。|
| **S**ecure **Sh**ell (**SSH**)|       22          |      该协议用于通过基于文本的管理界面安全登录系统。 |
| **H**yper**T**ext Transfer Protocol (**HTTP**)|         443        |         该协议为万维网 (WWW) 提供支持！ 您的浏览器使用它来下载网页的文本、图像和视频。        |
| **H**yper**T**ext **T**ransfer **P**rotocol **S**ecure (**HTTPS**) |445         |   该协议与上面的完全相同； 但是，安全地使用加密。             |
| **S**erver **M**essage **B**lock (**SMB**)|445|            该协议类似于文件传输协议 (FTP)； 但是，除了文件，SMB 还允许您共享打印机等设备。     |
| **R**emote **D**esktop **P**rotocol (**RDP**)|3389|          该协议是一种使用可视化桌面界面登录系统的安全方式（与 SSH 协议的基于文本的限制相反）。       |

![[Pasted image 20221217143222.png]]

# Task 6 Continue Your Learning: Extending Your Network

总结
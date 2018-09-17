---
title: 7 TELNET and SSH
date: 2018-04-17 16:26:29
category: Computer_Network
tags: [Application Layer]
---
<font size=6>终端网络与安全壳
<!--more-->

---
<font size=5>终端网络 (terminal network, TELNET) : 
<font size=3>TELNET是一个远程登录的协议,TELNET需要登录用户名和密码,但并不意味着用户名和密码是不会被黑客所盗取。因为用户名和密码都是明文，并没有进行加密。正是因为如此，TELNET的使用在另一个叫做安全壳的协议而减少。

在本地登录中，用户在终端中输入，经过终端驱动，将输入发给操作系统。而远程登录中，用户通过终端驱动发给操作系统再发给TELNET客户机，然后发往TELNET服务器，但是远程操作系统并不能直接从服务器接收报文，所以增加了一个伪终端驱动 (pseudoterminal dirver) 从服务器获取报文发给远程操作系统。
<br/>

<font size=5>安全壳 (secure shell, SSH) : 
<font size=3>SSH最原先是用来代替TELNET的协议，但在现在SSH可用于很多方面比如远程登录和文件传输。SSH有三个组件 : 
- SSH transport-layer protocol (SSH-TRANS) : 因为TCP不是一个安全传输层协议，所以再TCP的顶端加入了SSH-TRANS，TCP先建立一个非安全连接，然后交换安全参数建立安全通道于连接上。
- SSH authentication protocol (SSH-AUTH) : 在安全通道建立后，服务器与客户机互相认证。
- SSH connection protocol (SSH-CONN) : 在前两个协议完成后，SSH-CONN创造多个逻辑通道用于不同目的。

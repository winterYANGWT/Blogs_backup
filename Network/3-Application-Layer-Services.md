---
title: 3 Application Layer Services
date: 2018-03-27 19:44:59
category: Computer_Network
tags: [Application Layer]
---
<font size=6>应用层服务，应用层模式，套接字
<!--more-->

---
<font size=5>应用层服务 : 
<font size=3>应用层处于TCP/IP协议组的顶层，提供了程序对用户的服务，该层的服务建立了逻辑连接。
<br/>

<font size=5>客户机-服务器模式 (client-server paradigm, C/S paradigm) : 
<font size=3>C/S模式是最为流行的应用层模式。

在C/S模式里，服务器需要持续不断地工作，等待着客户机程请求。客户机可以在需要服务时才工作。该模式存在的问题就是服务器需要有着强大的性能和健壮性，当大量的客户机同时寻求服务，服务器可能会超过它的能力。
<br/>

<font size=5>套接字 (socket) : 
<font size=3>为了实现客户机与服务器之间的交流，我们可以使用叫做socket的API进行编程。

服务器认为socket是客户机的发送一个请求并需要返回回应，客户机认为socket是服务器接受请求并给予回应。在客户机和服务器之间通信需要一对套接字地址 (socket address)，本地地址 (local address) 和远程地址 (remote address)。socket地址由32位的IP地址和16位的端口号两部分组成。

服务器和客户机使用下面的方法来获得套接字地址来进行交流 : 
- 服务器 : 
    - 本地地址 : 服务器的socket本地地址由操作系统来获得。操作系统知道服务器的IP地址，若服务器是遵循网络标准，则端口地址已经确定。比如HTTP的端口地址就是80，若不遵循网络标准，设计者可以为其指定一个端口地址。
    - 远端地址 : 服务器的socket远端地址由客户端发送的socket来获得。
- 客户机 : 
    - 本地地址 : 客户机的socket本地地址由操作系统获得。操作系统知道客户机的IP地址，其端口地址由会被暂时分配。操纵系统需要检查该端口是否被占用。
    - 远程地址 : 有时客户机已经知道了服务器的地址，比如，一款网络游戏，其服务器地址就已经被赋予。在其他情况，端口地址在标准协议下已经广为人知，但是不知道IP地址，这时服务器就会有一个标识名，叫做统一资源定位器 (uniform resource locator, URL) 比如 www.xxx.yyy  xxx@yyy.zzz。DNS就会将URL解析为IP地址。就像电话号码本，将人名对应电话号码。我们将再下一节描述URL。
    
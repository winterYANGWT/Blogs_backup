---
title: 2 Protocol Layering
date: 2018-03-17 00:48:16
category: Computer_Network
tags: []
---
<font size=6>协议分层，TCP/IP
<!--more-->

---
<font size=5>协议层 (protocol layering) : 
<font size=3>我们将网络分为几个层次，分层让我们将复杂的网络分解成许多个简单的任务，当其中某层需要修改，我们只需修改该层即可，无需重新构建整个网络结构。这种思想被我们称之为模块化 (modularity)。

在模块化的思想中，每一层可看作一个黑盒。向黑盒输入，然后从黑盒获取输出。模块化使我们能够自顶向下的设计网络，同时，模块化意味着我们可以灵活，优雅地替换不同的模块。


协议分层需要遵守两个准则 : 
- 如果我们需要双向交流，需要使每一层具有正向和反向输入输出。例如 : 若将文本进行加密成密文，则该层也能将对密文解密成文本。
- 在同一层的两端的物体应该是相同的。因为我们在每一层的两端是逻辑连接的。在直觉上，当我们发送文本时，可以无需考虑其他层的工作，认为我们直接进行了连接从而传递了文本。
<br/>

<font size=5>TCP/IP协议组 : 
<font size=3>TCP/IP协议组是现如今最为广泛使用的协议组。在原本的协议中分为四层，为深入学习，则加入一层变为五层。这五层是 : 
- 应用层 (application layer) : 应用层中传输的对象是报文 (message),应用层有以下内容 : 
    - 超文本协议 (Hypertext Transfer Protocol, HTTP)
    - 万维网 (World Wide Web, WWW)
    - 简单邮件传输协议 (Simple Mail Transfer Protocol, SMTP)
    - 文件传输协议 (File Transfer Protocol, FTP)
    - 终端网络 (Terminal Network, TELNET)
    - 安全壳 (Secure Shell, SSH)
    - 简单网络管理协议 (Simple Network Management Protocol, SNMP)
    - 域名系统 (Domain Name System, DNS)
    - 网络组管理协议 (Internet Group Management Protocol, IGMP)
- 传输层 (transport layer) : 传输层传输的对象是数据段 (segment),传输层有以下内容 : 
    - 传输控制协议 (Transmission Control Protocol, TCP)
    - 用户数据报协议 (User Datagram Protocol, UDP)
    - 流控制传输协议 (Stream Control Transmission Protocol, SCTP)
- 网络层 (network layer) : 网络层传输的对象是分组 (packet) 网络层有以下内容 :  
    - 网络协议 (Internet Protocol, IP)
    - 网络控制信息协议 (Internet Control Message Protocol, ICMP)
    - 网络组管理协议 (Internet Group Management Protocol, IGMP)
    - 动态主机配置协议 (Dynamic Host Configuration Protocol, DHCP)
    - 地址解析协议 (Address Resolution Protocol, APR)
- 数据链路层 (data-link layer) : 数据链路层传输的对象是帧 (frame) TCP/IP并没有指定数据链路层的协议，可以使用任何标准协议。
- 物理层 (physical layer) : 物理层传输的对象是位 (bit)。

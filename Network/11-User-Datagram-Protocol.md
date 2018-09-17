---
title: 11 User Datagram Protocol
date: 2018-05-23 15:35:15
category: Computer_Network
tags: [Transport Layer]
---
<font size=6>用户数据报协议
<!--more-->

---
<font size=5>用户数据报协议 (User Datagram Protocol, UDP) : 
<font size=3>UDP是一个无连接，不可靠的传输层协议。在IP的基础上除了提供程序与程序之间的交流之外什么服务都没有提供。但是UDP是一个简单的协议且有较小的开销，在发送一些较小的信息时，使用UDP会比TCP减少发送方和接收方的交互。

UDP的分组，也叫数据报，有固定8个字节大小的头，头分成4个区域，每个区域为2个字节。前面的两个区域指定了源端口和目的端口。第三个区域指定了整个数据报的大小 (字节为单位)。第四个区域为校验和。因为第三个区域为16位，也就是我们的数据报大小可为 (8-65535字节)，但是应为IP报文的大小最大也为65535字节，所以我们的总长度一般会比65535字节要小。下图为数据报的格式 : 
![User datagram packet format](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%95%B0%E6%8D%AE%E6%8A%A5%E6%A0%BC%E5%BC%8F.png)
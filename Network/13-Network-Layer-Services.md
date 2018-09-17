---
title: 13 Network Layer Services
date: 2018-05-26 21:54:36
category: Computer_Network
tags: [Network Layer]
---
<font size=6>网络层服务
<!--more-->

---
<font size=5>网络层服务 : 
<font size=3>网络层由源主机，目标主机，和许多路由器组成。

网络层提供了封装和解封装服务。源主机将从传输层的分组进行封装发给数据链路层。目标主机将从数据链路层得到的分组解封并发给传输层。其中路由器不需要解封和封装，除非分组太大需要进行分段。源主机不允许修改得到的数据，除非数据太大需要进行分段。如果数据被分段，目标主机也需要等到所有分段到达。

网络层提供了路由的服务，它的责任是负责将分组从源主机路由到目标主机。物理网络是由许多网络和连接它们的路由器组成。这也意味着从源主机到目标主机有着不止一个路由器。网络层有责任尽可能找到最好的路由线路进行路由。在今日的互联网，使用路由协议来帮助路由器实现这个服务。

路由器使用转发表或路由表来进行转发。当一个路由器从一个与之连接的网络收到一个分组时，路由器使用分组的头中的一部分信息对转发表进行查找来找到对应的转发方向，然后将分组转发到对应的网络。

网络层并未像传输层一样提供错误控制，一个原因就是分组在网络层需要被经常分段，实现错误控制会十分低效。但却在分组的头加上了校验和来控制头的错误。虽然网络层并未直接提供错误控制，但是提供了一个辅助协议，ICMP提供了一些错误控制。

网络层也并未提供流控制，第一个原因是，网络层没有错误控制，接收方的工作简单很少会被数据淹没。第二个原因是上层协议能够实现缓冲区和流控制，在网络层实现流控制让网络层变得复杂低效。

网络层提供了拥塞控制，但并未在互联网中实现。
<br/>

<font size=5>分组交换 : 
<font size=3>
---
title: 1 Overview Of The Internet
date: 2018-03-10 00:34:30
category: Computer_Network
tags: []
---
<font size=6>局域网，广域网，互联网和因特网
<!--more-->

---
<font size=5>局域网 (local area network, LAN) : 
<font size=3>LAN一般是私有的且用来连接一个简单网络所有的主机 (host)，这个网络可以小到两台电脑和一台打印机，大到一个公司的网络。

每一个主机在局域网中有一个身份 (identifier)，一个包 (packet) 从源地址发生到目标地址。在以前，一个网络中的所有主机都会接收到包，然后除了目标，其他主机都将会将这个包丢掉。而现在交换机 (switch) 能够识别目标的地址 (address)，仅有目标能够收到这个包。这样大大地减轻了网络的负担。
<br/>

<font size=5>广域网 (wide area network, WAN) : 
<font size=3>LAN和WAN的区别最大在于其规模的限制。

在今天，WAN有两大类 : 
- 点对点WAN (point-to-point WAN) : 点对点WAN通过传输介质连接两个不同的设备。
- 交换式WAN (switched WAN) : 交换式WAN设备连接数量超过两个，我们可以说交换式WAN是由许多交换机所连接的许多点对点WAN。
<br/>

<font size=5>互联网 (the internet) : 
<font size=3>目前，单独的LAN和WAN都很少见，这些网络相互连接成为了互联网。

例如 : 可以有多个小型的LAN，他们由WAN连接。每个LAN内的设备可以通过LAN内部连接，而LAN中的设备可以通过WAN与其他LAN中的设备进行连接。

互联网有两类 : 
- 电路交换网络 (circuit-switched network) : 电路交换网络处于活动和未活动状态中，只有在两边的设备都处于连接时，电路交换网络才是有效率的。
- 分组交换网络 (packet-switched network) : 与电路交换网络不同的是，分组交换网络使用包的数据块进行交流。分组交换网络能将包存入队列，并持续分组发送。这样能够提高网络线路的使用效率，减少了网络连接的成本，但是可能产生一些延迟。
<br/>

<font size=5>因特网 (the Internet) : 
<font size=3>最著名的互联网就是英特网。因特网由数以万计的网络相组成。

在因特网的顶层，有着叫做主干网络 (backbone) 的大型网络，这些主干被像电信，联通这些公司所拥有且使用对等点 (peerint point) 的交换系统连接。在第二层，有一些小一些的网络叫提供商网络 (provider network)。提供商网络会与主干网络和其他提供商网络连接。在下一层就是客户网络 (customer network)。客户网络处于互联网的边缘。主干网络和提供商网络统称为网络服务供应商 (Internet Service Provider)。

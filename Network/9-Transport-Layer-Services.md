---
title: 9 Transport Layer Services
date: 2018-04-23 19:52:20
category: Computer_Network
tags: [Transport Layer]
---
<font size=6>传输层服务
<!--more-->

---
<font size=5>传输层服务 : 
<font size=3>传输层在应用层与网络层之间。提供了应用层之间程序对程序的交流的服务。该层建立了逻辑连接。

什么是程序对程序的交流?将一个应用层的程序看作使用传输层服务的一个实体，在应用层中有着许多的实体，将信息传递到正确的程序就是程序对程序的交流。
<br/>

<font size=5>传输层地址-端口 (port numbers) : 
<font size=3>怎么实现程序与程序的交流呢?如今的操作系统都支持多用户和多程序环境，一台计算机可以运行多个程序。我们使用端口来进行确认程序的身份。

在TCP/IP协议组里，端口是一个16位的整数，从0到65535。客户机程序使用临时端口。为了使得程序能正常工作，临时端口建议大于1023。服务器程序端口不能被随机选择，否则客户机程序不知道它想使用服务的端口。TCP/IP协议组提供了通用的端口。

ICANN将端口分为了三部分 : 
- 知名端口 (well-known ports) : 0到1023被ICANN指定和控制。
- 注册端口 (registered ports) : 1024到49151没有被ICANN指定和控制，但可以在ICANN注册来防止重复。
- 动态端口 (dynamic ports) : 49152到65535没有被控制和注册，可以用于私有或临时窗口。
<br/>

<font size=5>封装与解封 (encapsulation and decapsulation) : 
<font size=3>在发送端，根据传输层协议程序会将在报文加上一部分socket地址和一些信息进行封装。传输层接收并加上传输层头。在接收端，传输层头被丢弃，报文被发往程序。
<br/>

<font size=5>复用和解复用 (multiplexing and demultiplexing) : 
<font size=3>在发送端，传输层把来自不同程序的报文收封装为分组，称之为复用。在接收端，传输层将不同的分组解封发往不同的程序，称之为解复用。
<br/>

<font size=5>流控制 : 
<font size=3>在传输过程中，有一个发送方发送数据，同时有一个接收方接收数据。当发送方发送数据的能力大于接收方接收数据的能力，接收方就会被数据淹没，导致分组丢失。当发送方发送数据的能力小于接收方接收数据的能力，接收方就得等待数据，导致效率变低。

发送方与接收方的传输有两种方式。第一种是发送方发送数据且没有收到接收方的请求，这种方式叫做推。第二种是发送方收到接收方的请求后发送数据，这种方式叫做拉。当使用推这种传输方式可能会发生数据淹没，所以需要流控制。而使用拉时，接收方发送请求时已经做好了接收准备，所以不需要流控制。

发送方应用层程序将报文推给发送方传输层协议，发送方传输层协议将数据段推给接收方传输层协议，而接收方应用层程序将报文从接收方传输层拉过来。所以这个过程需要使用2次流控制。一次在发送方的应用层程序和传输层协议之间，另一次在发送方的传输层协议和接收方的传输层协议之间。

流控制中比较流行的方法就是使用缓冲区 (buffer)。在发送方和接收方设置缓冲区。当发送方传输层协议的缓冲区满了，就通知应用层程序停止传输数据。接收方传输层协议的缓冲区满了之后就通知发送方传输层协议停止传输数据。
<br/>

<font size=5>错误控制 : 
<font size=3>在传输层下的网络层是不可靠的。当需要可靠的传输时，就需要支持可靠传输的传输层协议。可靠的传输需要加入错误控制 : 
- 检查和丢弃错误的分组。
- 保持丢失和丢弃的分组的跟踪，并且做到重发分组。
- 识别重复分组并丢弃他们。
- 缓存失序分组直到缺失分组到达。

在错误控制中，我们假设应用层与传输层之间不会发生错误，只需讨论传输层发送方和接收方的错误控制。错误控制一般交给接收方来管理。

错误控制要求传输层发送方知道哪些分组需要重传，传输层接收方知道哪些分组是重复的或已经失序到达。使用序列号就可以完成实现上面的需求。在传输层发送的分组加上一个区域用为序列号，这样传输层接收方就可以要求发送方重传，也可以检测重复的分组和识别失序到达的分组。如果用作序列号的区域有m位，则序列号的范围是$0$到$2^m-1$。

在错误控制中可以用正信号和负信号，但在可靠数据传输 (reliable data transfer, rdt) 中可以只使用正信号也就是确认 (acknowledgement, ACK) 来进行错误控制。当发送方发送一个分组，计时器开始计时。接收方接收到正确的分组后，返回一个ACK。当ACK没有在计时器终止前到达，则重发这个分组。

![sliding window](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3.png)

如上图可见，我们将每一个序列号看成其中的一个切片，同时缓冲区就可以看出是一组连续的切片，也称为滑动窗口。在发送方发送一个分组，对应的序列号被标记。当窗口所有的序列号都被标记时，意味着缓冲区已满，无法从应用层接收更多的报文。当ACK到达时，对应序列号被取消标记，若在窗口的第一个序列号被取消标记，窗口就开始移动。
<br/>

<font size=5>拥塞控制 : 
<font size=3>在任何有等待的系统里就有可能出现拥塞。当向网络发送分组的数量大于网络能处理分组的能力时就会出现拥塞。在后面会继续介绍拥塞控制。
<br/>

<font size=5>无连接服务和面向连接服务 : 
<font size=3>传输层协议提供了两种服务 : 
- 无连接服务 : 在无连接服务中，应用层程序将报文分为可被传输层接受大小的块，并一个一个发往接收方传输层。其中每个块都是没有任何关联的单元。当块按序到达时，传输层正确处理。但是因为每一个块都是独立的，一旦发生失序传输，就会产生错误。但是没有流控制，错误控制，拥塞控制的无连接服务效率比较高。
- 面向连接服务 : 在面向连接的服务中，在传输数据前需要建立一个逻辑连接，传输数据后需要断开连接。在面向连接服务中，我们需要实现流控制，错误控制，拥塞控制。

<font size=5>有限状态机 (finite state machine, FSM) : 
<font size=3>无论是无连接服务还是面向连接服务，其行为都可以很好地用FSM来描述。传输层可以看作有着有限状态。每个FSM一直处于一个状态，直到事件发生。每个事件都有两个反应 : 定义将被执行的动作列表和确定下一个状态。必须有一个初始状态，当FSM启动时就处于初始状态。
如上图所示的FSM，使用一条横线来分开事件和动作，事件在线上，动作在线下。
![finite state machine](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA.jpg)
我们可以认为无连接服务是一个只有一个建立状态的FSM，一直处于准备发生和接收传输层的分组。而面向连接服务则有许多状态的FSM。
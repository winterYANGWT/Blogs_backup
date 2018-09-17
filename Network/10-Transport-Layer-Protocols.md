---
title: 10.Transport_Layer_Protocols
date: 2018-05-14 13:14:35
category: Computer_Network
tags: [Transport Layer]
---
<font size=6>传输层协议
<!--more-->

---
<font size=5>一个简单协议 : 
<font size=3>在此，我们先从一个最简单的传输层协议开始，逐渐增加复杂性。为了简单讨论，我们认为这些协议都是单向协议，也就是分组都是发往一个方向。

我们的第一个协议是一个简单的无连接协议，没有流控制和错误控制。我们也假定接收方能够立即处理收到的分组，也就是接收方不会被发来的分组给淹没。在这个简单协议里，传输层发送方从应用层得到报文，并将它封装后发给传输层接收方，传输层接收方收到分组后，将其解封装并发给应用层。下图是简单协议的FSM : 
![simple protocol's FSM](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E7%AE%80%E5%8D%95%E5%8D%8F%E8%AE%AE%E7%9A%84%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA.png)
<br/>

<font size=5>停等协议 (stop and wait protocol) : 
<font size=3>我们的第二个协议是停等协议，它是一个面向连接协议，使用流控制和错误控制。发送方和接收方使用大小为1的滑动窗口。发送方一次发送一个分组，在发下一个分组之前需要等待ACK，为了检查分组是否损坏，我们在每一个分组加上一个校验和，当接收方收到分组并发现校验和不正确，就将这个分组丢弃。发送方未收到ACK，认为这个分组损坏或丢失，就重传这个分组，直到ACK到达。

在停等协议中，为了减小序列号的长度，我们可以只用两个数字。下面讨论三种情况 : 
- 分组0 (1) 正确到达接收方，接收方返回ACK。ACK到达发送方，发送方发送分组1 (0)。
- 分组0 (1) 损坏或丢失，发送方在超时后重传，接收方返回ACK。
- 分组0 (1) 正确到达接收方，接收方返回ACK。但是ACK损坏或丢失，发送方超时重传。

关于ACK，我们令ACK的数字为下一个需要被传输的分组的序列号。比如，当分组0正确到达接收方，接收方返回ACK1。分组1正确到达接收方时，ACK0被返回。

下图是停等协议的FSM : 
![stop and wait protocol's FSM](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E5%81%9C%E7%AD%89%E5%8D%8F%E8%AE%AE%E7%9A%84%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA.png)

当带宽大，延迟高的情况下，停等协议的效率十分低下。比如在$1\times10^6$bit带宽和$2\times10^{-2}$的延迟下发送$1000$bit的分组，其使用率是$\frac{1000}{1\times10^6\times2\times10^{-2}}\times100\%=5\%$。
<br/>

<font size=5>回退N协议 (Go-Back-N protocol, GBN) : 
<font size=3>为了增强传输效率，需要传输许多分组来使通道处于繁忙状态。GBN正是这样的一个协议。

GBN发送方可以在收到ACK之前发送许多的分组，GBN接收方只能缓存一个分组。在GBN协议中，ACK序号是累计的也是期待收到下一个分组的序列号。

![Send window](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/Send_Window.png)
GBN协议的发送窗口的大小最大是$2^m-1$，其中$m$是序列号的位的大小。上图是一个大小为7，$m$为3的发送窗口。我们使用$S_{size}$表示滑动窗口的大小，$S_f$表示窗口中第一个被发送，未收到ACK的序列号，$S_n$表示窗口中将被发送的序列号。当收到一个ACK其序号处于$S_f$到$S_n$中，则窗口向右滑动到$S_f$为收到ACK的序号。

![Receive window](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/Receive_Window.png)
GBN协议的接收窗口大小是1。接收方只接收指定分组，失序的分组将会被丢弃，等待重发。我们使用$R_n$来表示窗口中等待的分组的序号。当序号为$R_n$的分组收到时，窗口向右滑动到$R_n=R_n+1$,发送ACK的序号是$R_n$。

在GBN协议中我们只需要一个计时器就够了，因为我们序号为$R_n$的分组的计时器总会第一个超时，接着就会重发所有已发送，但未确认的分组。这也是这个协议被称为回退N协议的原因。下图为GBN协议的FSM : 
![GBN protocol's FSM](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E5%9B%9E%E9%80%80N%E5%8D%8F%E8%AE%AE%E7%9A%84%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA.png)

接下来，我们来了解为什么GBN协议的发送窗口的最大大小为$2^m-1$。假设窗口大小为$4$，$m=2$。当发送方发送了分组0，1，2，3，接收方都收到了。随后发送ACK1，ACK2，ACK3，ACK0。假设ACK1，ACK2，ACK3，ACK0都丢失。发送方会重复分组0，1，2，3，接收方会将重发的分组认为是新的数据而选择接收。这样就产生了错误接收。
<br/>

<font size=5>选择重传 (Selective-Repeat protocol, SR) : 
<font size=3>在GBN协议，接收方的工作很简单，不需要缓存失序的分组而是直接丢弃。每当一个分组丢失，发送方需要重传所有分组，即使失序的分组能够正确到达。这种情况导致了十分低下的效率，而且当因为网络拥塞导致丢分组，重发所有分组会让网络拥塞的情况更加严重。所以另一个协议，SR协议，可以选择性地重传丢失的。

与GBN协议不同的是发送窗口的最大大小是$2^m-1$,接收窗口的大小也是$2^m-1$。

![SR protocol's send window](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E9%80%89%E6%8B%A9%E9%87%8D%E4%BC%A0%E7%9A%84%E5%8F%91%E9%80%81%E7%AA%97%E5%8F%A3.png)
SR协议的发送窗口大小为$2^{m-1}$。

![SR protocol's receive window](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E9%80%89%E6%8B%A9%E9%87%8D%E4%BC%A0%E7%9A%84%E6%8E%A5%E6%94%B6%E7%AA%97%E5%8F%A3.png)
SR协议的接收窗口大小也是$2^{m-1}$。SR协议将失序到达的分组缓冲，最后一起交付给应用层。

SR协议会为每一个发送的分组设置计时器，当计时器超时，只有对应的分组会进行重传。这里GBN协议和SR协议的不同之处在于GBN协议将所有发送，但未确认的分组看作一个整体，SR协议将他们看作分离的个体。而在GBN中ACK的序号是累积的，当一个ACK到达时，可以认为这个ACK序号前面对应的分组都已被正确接收。在SR协议中ACK序号则代表了对于序列号的单个分组正确到达。下图为SR协议的FSM : 
![SR protocol's FSM](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C/%E9%80%89%E6%8B%A9%E9%87%8D%E4%BC%A0%E7%9A%84%E6%9C%89%E9%99%90%E7%8A%B6%E6%80%81%E6%9C%BA.png)

为什么发送方和接收方的滑动窗口最大大小为$2^{m-1}$?假设窗口大小为$2$，$m=2$。当发送方发送了分组0，1，2，接收方都收到了。ACK0，ACK1，ACK2都丢失了。此时接收窗口为[3][0][1],发送窗口为[0][1][2]。当发送方重发分组0时，接收方会将其认为是新的分组0，而导致错误接收。
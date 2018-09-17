---
title: 6 E-mail protocols
date: 2018-04-16 21:34:54
category: Computer_Network
tags: [Application Layer]
---
<font size=6>邮件协议群
<!--more-->

---
<font size=5>电子邮件 : 
<font size=3>电子邮件并不像前面提到的HTTP和FTP，电子邮件被认为是单边传输。比如A向B发送了一个邮件，但是B可以回复也可以不回复。此外上个例子中B也并不需要一直等待邮件的接收。这也就是说C/S模式需要其他的实现手段。

电子邮件的通信需要三个代理 : 
- 用户代理 (user agent, UA)
- 邮件传输代理 (mail transfer agent, MTA)
- 信息访问代理 (message access agent, MAA)

邮件传输的步骤如下 : 
1. A使用UA写邮件并通过MTA客户机发给A的邮件服务器中的服务器，邮件服务器使用一个队列存储待发送的邮件.
2. 接着通过MTA将邮件从A的邮件服务器发送到B的邮件服务器。此时需要两个MTA，一个为客户机，另一个为服务器。
3. B可以使用UA读取已收到的邮件，然后B使用MAA客户机请求B的邮件服务器中的MAA服务器返回报文。

邮件的格式 : 邮件有信封 (envelope) 和 报文 (message)。信封包含发送者地址，收信者地址以及其他信息。报文有报文头 (header) 和报文体 (body),报文头指明了发送者，接收者，时间，主题等，信息体是正文。

邮件地址是本地部分和域名使用@连接而成。例如local_part@domain_name.本地部分对应了一个叫用户邮箱的特殊文件。域名对应了邮件服务器。
<br/>

<font size=5>简单邮件传输协议 (simple mail transfer protocol, SMTP) : 
<font size=3>SMTP用于用户和邮件服务器和邮件服务器之间的MTA传输邮件。SMTP使用命令与回应的方式进行通信。命令与回应可以查询RFC文档。SMTP使用端口25。
<br/>

<font size=5>邮局协议 (post office protocol,version 3, POP3) 和 网络邮件访问协议 (Internet mail access protocol,version 4, IMAP4) : 
<font size=3>POP3简单但是功能受到了限制。IMAP4与POP3相似，但是功能更多，所以会更加地强大且复杂。
- POP3 : 当用户需要从邮件服务器的邮箱下载邮件时，客户机MAA与客户机MAA建立连接并服务器使端口110。POP3有两种模式delete和keep。使用delete模式，邮件会在现在后删除，keep模式会依然保存在邮件服务器中。
- IMAP4 : IMAP4支持以下功能 : 
    - 用户能下载前检查邮件头。
    - 用户能在下载前通过字符串搜索邮件内容。
    - 用户能部分下载邮件。
    - 用户能创造、删除、重命名邮件服务器上的邮箱。
    - 用户能创建邮箱的层次。
<br/>

<font size=5>多用途网络邮件扩展 (multipurpose Internet mail extensions, MIME) : 
<font size=3>MIME是一个支持非ASCII数据发送的补充协议。MIME在UA将非ACSII数据转换为NVT ASCII并传给客户机MTA。在MAA传回UA又NVT ASCII将数据转回非ASCII数据。

MIME定义了五个头 : 
- MIME-Version
- Content-Type
- Content-Transfer-Encoding
- Content-ID
- Content-Description
<br/>

<font size=5>基于Web的邮件 : 
<font size=3>如今Web可以收发邮件，基于Web的邮件又两种情形 : 
- 发送邮件时使用SMTP让浏览器与邮件服务器传输，使用HTTP接收邮件。
- 发送邮件与接收邮件都使用HTTP。

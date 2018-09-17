---
title: 5 FTP
date: 2018-04-10 21:15:35
category: Computer_Network
tags: [Application Layer]
---
<font size=6>文件传输协议， 简单邮件传输协议以及其他的邮件协议
<!--more-->

---
<font size=5>文件传输协议 (File Transfer Protocol, FTP) : 
<font size=3>FTP是一个TCP/IP suite提供用于传输文件的协议。HTTP也可以传输文件，但是使用FTP在传输大型文件时将会是更好的一个选择。

FTP的基本模型中，客户机又三个组件 : 用户接口 (user interface),客户机控制程序 (client control process), 客户机数据传输程序 (client data transfer process)。服务器有两个组件 : 服务器控制程序 (server control process), 服务器据数据传输程序 (server data transfer process)。命令与数据传输的分离让FTP变得高效。

FTP中控制连接与数据传输连接有着不同的生命周期。控制连接贯穿整个生命周期，数据传输连接在整个生命周期中可以开关多次。控制连接使用端口21，数据传输连接使用端口20.

FTP的控制连接通过使用命令和回应进行交流，客户机向服务器发送命令，服务器返回回应给客户机。命令与回应可查询RFC文档。

FTP的数据传输连接需要三个属性 : 
- 数据结构 (data structure) : 数据结构中有三种结构 : 
    - 文件结构 (file structure) : 文件结构为默认方式，没有结构，是一段连续的字节流。
    - 记录结构 (record structure) : 在记录结构中，文件被分为许多记录，这种结构仅用于文本文件。
    - 分页结构 (page structure) : 在分页结构中，文件被分为许多分页，每个分页都有其分页号和分页头。这些分页可以被随机访问或顺序访问。
- 文件类型 (file type) : FTP可以传输ASCII文件，EBCDIC文件，图像文件。
- 传输模式 (transmission mode) : 传输模式有三种模式 : 
    - 流模式 (stream mode) : 流模式是默认的传输模式，数据通过一段连续的字节流传输。 
    - 块模式 (block mode) 块模式中将文件分为块。每个块都加上3字节的头，第一个字节叫块描述符 (block descriptor)。剩下两个字节描述块的大小 (单位为字节)。
    - 压缩传输模式 (compressed mode)

---
title: 2 Information Storage
date: 2018-09-20 20:56:46
category: Computer_System
---
<font size=6>信息存储
<!--more-->

---
<font size=5>信息存储
<font size=3>相比于访问单个位，大多数计算机更适合将8位的块，也就是字节作为内存中最小的访问单位。从机器的角度来看，程序将内存视为由字节组成的数组，也就是虚拟内存。每一个字节都有独一无二的地址被用来访问，所有可用地址组成了虚拟地址空间。虚拟地址空间只是一个概念，其实现是动态随机存储器、闪存、硬盘、其他硬件、操作系统软件的组合来为程序提供看似只有一块内存的虚拟试图。编译器和操纵系统会将内存空间拆分为多个可管理的单元来存储不同的对象 (数据、指令、控制信息等)，这个过程蕴含了许多机制。这些机制都是运行在虚拟地址空间上的。举个例子，我们知道，在C语言中一个整数、数据结构或其他对象的指针都指向数据在虚拟地址空间的首地址，C编译器会为每个指针附加上类型信息，来生成不同的代码访问数据。但是从机器的角度来看，这些信息并不实际存在。
<br/>

<font size=5>数据大小
<font size=3>字长是计算机单个周期内能够处理的最大操作数的位数长度，现在计算机基本为64位。字长也表明了一台计算机虚拟地址空间的大小。如果一台计算机的字长为$w$,这台计算机的虚拟地址空间的范围为$0$~$2^w-1$。64位的计算机可以运行64位和32位的程序，反之则不可行。
<br/>

<font size=5>寻址和字节顺序
<font size=3>一些程序对象可能占用多个字节，这时候我们需要讨论俩个问题。这个对象的地址是什么和对象在内存中的字节顺序。多字节的对象占用连续的地址空间，对象的地址是所占用的地址空间中的最小地址。字节顺序也有两种 : 
- 大端顺序 : 将最低有效字节存储在最高地址。
- 小端顺序 : 将最低有效字节存储在最低地址。
假设我们需要存储的数据为0x12345678,大端顺序和小端顺序的差别如下
![Computer_System_2_1_3](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_2_1_3.png.jpg?q-sign-algorithm=sha1&q-ak=AKIDPwQGFQ3v3nUXTrqh8rDGOV7WnrSW3LzK&q-sign-time=1548345754;1548347554&q-key-time=1548345754;1548347554&q-header-list=&q-url-param-list=&q-signature=a44d9038cb9937fa5c91b56346c55d034480acbe&x-cos-security-token=e1733d28c45754571a9fb94f99ae4250f06b0da810001)

不同的操作系统使用不同的字节顺序。大端顺序和小端顺序在技术上不存在优劣问题。对于大多数的用户，字节顺序是不可见的，所以并不需要关心字节顺序。但是有时字节顺序是一个大问题。第一种情况是使用网络与其他计算机进行交流时，计算机之间使用的字节顺序不同。所以在计算机网络编程时需要遵守网络标准字节顺序。第二种情况是在进行反汇编的时候需要注意字节顺序。第三种情况是在编写非正常的类型程序时，比如在C语言中的类型转换和联合，会导致数据类型和创建这个对象所使用的类型不同。

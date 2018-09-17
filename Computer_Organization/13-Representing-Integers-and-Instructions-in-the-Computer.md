---
title: 13 Representing Integers and Instructions in the Computer
date: 2018-08-21 18:40:20
category: Computer_Organization
---
<font size=6>计算机中整数与指令的表示
<!--more-->

---
<font size=5>无符号整数在计算机中的表示
<font size=3>数字在计算机中使用二进制来表示。无符号数没有负数值，位数为$b$的无符号数的大小取值范围位$0$到$2^b-1$。在整数中第$i$位的数字的值可以由下面这个公式来进行描述，$i$从0开始。
$$d \times 2^i$$
举个例子,$1101_2=13$。如果要对无符号数进行位数的扩展，只需要将扩展出的位上全部用0补满。
<br/>

<font size=5>有符号整数在计算机中的表示
<font size=3>有符号整数的表示方法有几种，目前使用最多的就是二进制补码的表示方法。位数为b的有符号数的大小取值范围位$-2^{b-1}$到$2^{b-1}-1$。位数为$b$的有符号数的大小可以用以下的公式来进行描述。
$$d_b \times -2^{b-1}+d_{b-1} \times 2^{b-2}+ \cdots +d_2 \times 2 + d_1 \times 2^0$$
比如$1101_2=-3$,我们还有一个简单的方法将得到一个数的相反数。将$x$的位数取反得到反码$\overline{x}$。因为$x+\overline{x}=-1$,所以$\overline{x}+1=-x$。也就是将x的每位取反后加1就可以得到该数的相反数。所以补码又被称为反码加一码。如果要对有符号数进行位数的扩展，就将扩展为全部用最高有效位进行补满。
<br/>

<font size=5>指令在计算机中的表示
<font size=3>人和计算机对指令有着不一样的看法，在计算机中指令的格式为高低电平，与数字的表示方法是一样的。为了与汇编语言进行区分，我们将使用数字进行表示的指令又被称为机器语言。所有的MIPS指令都是32位。前面提到MIPS有32个寄存器，所以需要5位来表示寄存器。`$s0`到`$s7`对应寄存器编号为16到23，`$t0`到`$t1`对应寄存器编号为8到15。MIPS指令有它自己的布局格式。第一类格式为R型
![Computer_Organization_Figure_2.5_R-Format_MIPS_Field](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BB%84%E6%88%90%E5%8E%9F%E7%90%86/Computer_Organization_Figure_2.5_R-Format_MIPS_Field.png)

第二类格式为I型
![Computer_Organization_Figure_2.5_I-Format_MIPS_Field](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BB%84%E6%88%90%E5%8E%9F%E7%90%86/Computer_Organization_Figure_2.5_I-Format_MIPS_Field.png)

首先对其字段进行一些说明 : 
- op : 指令的基本操作,也被称为操作码 (opcode)。
- rs : 第一个源操作数寄存器。
- rt : 第二个源操作数寄存器。
- rd : 用于存放结果的寄存器。
- shamt : 位移量。
- funct : 功能码。用于指明op字段中的变式。

加法算数运算的指令为R型。因为加法运算指令需要三个寄存器。但是载入和常数加法运算这些指令，需要指明常数的大小或内存的地址，如果使用R型的格式，常数或地址就不能大于32，所以使用I型的16位来进行表示常数和地址，其范围就扩大到了$\pm 2^{15}$或32768字节。对于不同需求的指令，使用不同的格式，但是却保证了指令的总长为32位。这就是硬件设计的第三条原则 : 优秀的设计需要适合的折中方案。
---
title: 14 Logical Operations and Instructions for Making Decisions
date: 2018-09-06 20:06:17
category: Computer_Organization
---
<font size=6>逻辑操作和决策指令
<!--more-->

---
<font size=5>逻辑操作
<font size=3>最开始的计算机只能完成整个字的操作，但是在之后的计算机能够支持对字的一部分或者单个位的操作。检测8位的字符就是这种操作的一种。为了简化对字中若干位进行打包和拆包的操作，高级编程语言和指令集加入了一些指令，这些指令被称为逻辑操作。下图是C、Java、MIPS的逻辑操作 : 
![	Computer_Organization_FIGURE_2.8_C_and_Java_logical_operators_and_their_corresponding_RISC-V_instructions](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BB%84%E6%88%90%E5%8E%9F%E7%90%86/Computer_Organization_FIGURE_2.8_C_and_Java_logical_operators_and_their_corresponding_RISC-V_instructions.png)

第一类逻辑操作是移位。这种指令移动字中的所有位左移或右移，R类指令中的shamt就是用于指定位移量。
```assembly
sll $t2,$s0,4 #$t2=$s0<<4 bits, shamt=4
```

第二类操作是按位操作，如与，或，非，异或。其中非的按位操作并没有特定的指令，而是使用与0异或来实现非操作。
```assembly
and $t0,$t1,$t2     #$t0= $t1 & $t2
or $t0,$t1,$t2      #$t0= $t1 | $t2
xor $t0,$t1,$t2     #$t0= ~ ($t1 | $t2)
xori $t0,$t1,0      #$t0= ~ $t1
```
<br/>

<font size=5>决策指令
<font size=3>计算机区别于计算器之处就在于计算机能够做出决策。由于不同的输入数据和计算产生的值，不同的指令会被执行。高级编程语言使用if语句来表示决策，在MIPS的指令集有两种指令来实现if语句的功能。它们分别是beq和bne。
beq在两个操作数相同时跳转到对应标签
```assembly
beq $s0,$s1,L1      #go to L1 if $s0 equals $s1
L1: ...
```

bne在两个操作数不相同时跳转到对应标签
```assembly
bne $s0,$s1,L2      #go to L2 if $s0 doesn't equal $s1
L2: ...
```

MIPS还提供了无条件跳转指令j
```assembly
j L3        #go to L3
L3: ...
```

除了检测是否相等，在if语句中还经常出现大小比较。MIPS提供了slt指令来比较大小
```assembly
slt $t0,$s1,$s2     #$t0=1 if $s1 < $s2
```

一些高级编程语言还提供了switch语句来在众多分支中做出决策。switch最简单的实现方式就是将switch语句转换为一系列if-then-else语句。另外一种实现的方式就是将这些分支编码为一张表，也叫转移地址表。这样程序只需根据索引转移地址表就能做出决策。MIPS提供了寄存器跳转jr指令来进行无条件跳转到寄存器指定的地址，这条语句将会在以后进行提及。
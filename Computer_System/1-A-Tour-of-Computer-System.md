---
title: 1 A Tour of Computer System
date: 2018-07-05 14:04:45
category: Computer_System
---
<font size=6>计算机系统漫游
<!--more-->

---
<font size=5>什么是计算机系统
<font size=3>所谓计算机系统就是硬件和系统软件一齐工作来运行程序。系统的实现不断变化，但在其变化之下的概念却没有多少变化。所有计算机系统有着相同的硬件和软件来实现同样的功能。现在我们来深入理解计算机系统。
<br/>

<font size=5>信息就是位 (bit) +语境 (context)
<font size=3>对于一个C程序，其生命开始于其源程序 (也叫源代码)。程序员使用编辑器来编写程序并保存为文件。源文件就是一串位的序列，用一个8位的块来进行组织，这个块就是字节 (byte)，所以说源文件也是一段字节序列。大多数计算机系统使用ASCII码来表示文本字符。每一个字符大小位一个字节，且有一个十进制整数与其对应。完全使用ASCII码的文件为文本文件 (这里并未考虑Unicode)。其他文件为二进制文件。

这样就阐述了一个基础思想 : 系统内所有的信息 (磁盘上的文件，内存中的程序和数据，网络中传输的数据) 都使用一串的位来进行表示。这些信息的不同之处就在于我们怎么去看待它们，也就是语境。比如，对于同样的字节序列，我们使用整数，浮点数，字符串，机器指令等不同的看法去看待它，就会解读出不一样的信息。
<br/>

<font size=5>程序被其他程序翻译成不同格式
<font size=3>源代码能够很容易被人阅读，但为了能让它运行在系统上，源代码需要被其他程序翻译为低级机器语言的指令序列。这些指令被打包为可执行对象程序 (executable object program)。可执行对象程序在磁盘上存储格式为二进制文件。

将源文件翻译为对象文件的过程叫做编译，接下来我们以C的编译过程进行举例 : 
1. 预处理阶段 (preprocessing phase) : 预处理器将原来的C程序的预处理部分进行修改，执行预处理的命令。预处理阶段输出后缀为.i的文件。
2. 编译阶段 (complication phase) : 编译器将.i文件翻译为.s文件。.s文件包含了汇编语言。使用汇编语言的好处就在于它是公共输出语言，也就是不同的语言和不同的编译器都将生成一样的汇编语言。
3. 汇编阶段 (assembly phase) : 汇编编译器将.s文件翻译为机器语言指令，并打包成可重定位对象程序 (relocatable object program),并存储为.o文件。
4. 链接阶段 (linking phase) : 一个C程序可能包含了许多文件，最终程序需要将许多.o文件链接最终输出可执行对象程序。
<br/>

<font size=5>了解编译系统如何工作是有益的
<font size=3>对于简单的程序，我们完全可以依赖编译系统就能产生正确且高效的代码。但是程序员了解编译系统是非常有必要的 : 
- 优化程序性能 : 现代编译器都是很成熟的程序了，以致于不需要了解其内部工作方式就能写出高性能的代码。但是，为了做出好的代码选择，我们确实需要了解一些机器码和编译器的翻译方式。比如switch语句是否优于if-else?函数调用需要多少开销?while循环是否比for循环更加高效。指针引用比数组索引效率高?
- 理解链接时的错误 : 以经验来看，大多数烦人的问题一般出现在链接操作，尤其是在建立大型的软件系统。比如链接器报告无法解析引用是什么意思?静态变量和全局变量有什么差别?在不同的C文件中定义同名的全局变量会发生什么?静态库和动态库有什么不同之处?
- 避免安全漏洞 : 多年以来，缓冲区溢出漏洞在网络服务上经常出现，因为很少有程序员知道需要小心限制未结构化的数据格式与数据量。学习写出具有安全性的程序的第一步就是理解数据与控制信息存储在栈上的方式会引起的后果。
<br/>

<font size=5>处理器读取并解释存储在内存中的指令
<font size=3>完成了编译后，只需在shell中输入程序的名字就可以执行该程序。在执行程序的时候到底发生了什么呢？

首先我们需要了解对于一个系统来言，它的硬件组成是怎么样的呢?接下来我们就介绍一些基本的硬件组成。
- 总线 (buses) : 总线是贯穿整个系统的一系列的电子管线，携带信息的字节并在各个部件间传递。总线被设计传输固定大小的字节块，又被叫做字 (word)。字的大小现如今一般为32位或64位。
- 输入输出设备 (I/O devices) : 输入输出设备是系统与外界的连接。键盘，鼠标用于用户输入，显示器用于用户输出，磁盘用于长时间数据与程序的存储。我们的C程序也是存储于磁盘当中。
- 主存 (main memory) : 主存是一个暂时存储设备，用于处理器执行程序时存储程序与数据。在物理上，主存包括一系列动态随机方位内存芯片。在逻辑上，内存是一个字节的线性数组。每一个字节都有它自己独一无二的地址。一般来说，组成程序的每一条机器指令的字节数都不相同。
- 处理器 (processor) : 处理器解释存储在主存的指令，它的核心是一个字长大小的寄存器，又叫程序计数器。程序计数器指向机器指令。这些操作围绕着主存，寄存器，算数/逻辑单元 (ALU) 进行。一般来说，处理器会执行一下功能 : 
    - 加载 : 将字节或字从主存放入寄存器里，重写寄存器里的内容。
    - 存储 : 将字节或字从寄存器放回主存的某个地址里，重写主存中该地址的内容。
    - 操作 : 从两个寄存器的字放入ALU中，进行算数运算，放回寄存器中，重写寄存器的内容。
    - 跳转 : 从指令本身抽出一个字，将这个字放入程序计数器，重写程序计数器的内容。

在了解完系统的硬件组成后，我们开始大致了解运行程序后会发生一些什么。首先shell等待我们输入命令，在输入运行程序的指令后，shell程序将输入的每一个字符放入寄存器再放入内存当中。这个过程如下图 : 
![Computer_System_Figure_1.5_Reading_the _hello_command_from_the_keyboard](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_Figure_1.5_Reading_the%20_hello_command_from_the_keyboard.png)
shell程序通过一系列的指令将可执行文件的从磁盘读入内存当中。由于使用了一种叫直接内存访问的技术，文件可以无需处理器直接从磁盘进入内存。这个过程如下图 : 
![Computer_System_Figure_1.6_Loading_the_executable_from_disk_into_main_memory](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_Figure_1.6_Loading_the_executable_from_disk_into_main_memory.png)
然后处理器再执行代码里的机器指令。这个过程如下图 : 
![Computer_System_Figure_1.7_Writing_the_output_string_from_memory_to_the_display](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_Figure_1.7_Writing_the_output_string_from_memory_to_the_display.png)
<br/>

<font size=5>高速缓存至关重要
<font size=3>从上可知，系统花费了大量的时间来将信息从一处移动到凌一处。程序的机器指令存储再磁盘上。当载入程序的时候，这些指令从被拷贝到主存里。当处理器开始运行程序时，指令被拷贝到处理器中。程序在运行的时间里，这些移动花费的时间严重拖慢了程序真正的工作时间。根据物理法则，有更大容量的设备会更慢一些，而且高速设备的造价远高于同类型的低速设备。在一般的系统里，磁盘的大小一般比内存大1000倍左右，但是处理器从内存中读取一个字会比在磁盘里读快10000000倍。与此类似，一个寄存器文件可能就几百字节的信息，但是内存能有几十亿字节。处理器从寄存器中读取字会比在内存中读快100倍左右。而且随着半导体技术的发展，加快寄存器的速度比加快内存的速度更加容易，成本更低，寄存器和内存的之间的差距会更加地大。

为了解决这种差距，系统的设计师使用了高速缓存，一种更小，更快的存储设备，作为暂时的集结区域，存放处理器近期可能需要使用的信息。下图展示了高速缓存在计算机系统里扮演的角色 : 
![Computer_System_Figure_1.8_Cache_memories](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_Figure_1.8_Cache_memories.png)
这样系统就可以获得了一个较大，访问速度快的存储器。让高速缓存存放可能经常需要的数据，在内存中完成的操作都可以在更快的高速缓存内完成。

有了加入缓存的思想后，我们就可以对计算机的存储设备进行层次性划分。这个划分如下图 : 
![Computer_System_Figure_1.9_Hierarchy_of_memories](https://winteryangwt-1256492362.cos.ap-chengdu.myqcloud.com/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%B3%BB%E7%BB%9F/Computer_System_Figure_1.9_Hierarchy_of_memories.png)
在这张图里，每一层都是下面一层的缓存。理解了存储设备的层次化，程序员就可以利用缓存来提高程序的性能。
<br/>

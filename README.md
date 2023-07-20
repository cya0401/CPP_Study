# CPP_Study

## c++匿名函数(lambda表达式)的使用方法

[c++匿名函数(lambda表达式)的使用方法_吃素的施子的博客-CSDN博客](https://blog.csdn.net/feikudai8460/article/details/109624363)

#### 请说说ARM微处理器的特点。⭐⭐⭐⭐⭐

采用RISC架构的ARM微处理器一般具有如下特点：

1. **体积小**、**低功耗**、**低成本**、**高性能**；
2. 支持Thumb（16位）/ARM（32位）**双指令集**，能很好的兼容8位/16位器件；
3. 大量使用**寄存器**，指令执行速度更快；
4. 大多数数据操作都在**寄存器**中完成；
5. 寻址方式灵活简单，执行效率高；
6. **指令长度固定**；

除此以外，ARM体系结构还采用了一些特别的技术，在保证高性能的前提下尽量缩小芯片的面积，并降低功耗：

1. 所有的指令都可根据前面的执行结果决定是否被执行，从而提高指令的执行效率。
2. 可用加载/存储指令批量传输数据，以提高数据的传输效率。
3. 可在一条数据处理指令中同时完成逻辑处理和移位处理。
4. 在循环处理中使用地址的自动增减来提高运行效率。
5. 支持协处理器来扩展ARM的功能

[ARM体系架构概述 | 知识总结](https://dongka.github.io/2018/11/17/cpu/arm%E4%BD%93%E7%B3%BB%E6%9E%B6%E6%9E%84%E7%9A%84%E5%8F%91%E5%B1%95/)

RISC-V具有以下优点：

1.可模块化配置的指令集。 
2.支持可扩展的指令集 
3.一套指令集支持所有架构，基本指令集仅40余条指令，以此为共用基础，加上其他常用模块子集指令总指令集也仅几十条 
4.硬件设计和编译器非常简单

### arm体系的CPU工作模式：

1.用户模式(usr):正常的程序执行状态  
2.快速中断模式（fiq）:用于支持高速数据传输或者通道处理  
3.中断模式（irq）:用于普通中断处理  
4.管理模式（svc）:操作系统使用的保护模式  
5.系统模式（sys）:运行具有特权的操作系统的任务；  
6.数据访问终止模式（abt）:数据或指令与预取终止时进入该模式  
7.未定义指令终止模式（und）:未定义的指令执行时进入该模式；

## 什么是僵尸进程与孤儿进程

[什么是僵尸进程与孤儿进程_张维鹏的博客-CSDN博客](https://blog.csdn.net/a745233700/article/details/120715371)

## gdb几种设置断点的方式

[gdb几种设置断点的方式_gdb 断点_金士顿的博客-CSDN博客](https://blog.csdn.net/wojiuguowei/article/details/82386567)

gdb几种设置断点的方式  
方式1、根据函数名，查找符号（[symbol](https://so.csdn.net/so/search?q=symbol&spm=1001.2101.3001.7020)）设置断电  
此种方式最为简单，阅读源代码，了解函数如何调用，在需要暂停运行的函数入口进行断点设置。但并不是所有函数，任何时候都能设置断点的。比如优化后的静态函数，inline函数。在特定的情况下，通过函数名进行断点设置便不可为，而又需要查看运行时该函数的运行情况，这时就需要使用第二种方式。  
例子：b func_name

方式2、根据代码行位置设置断点  
当无法通过方式1进行设置断点，而又明确知道，程序运行到源代码文件中某个位置需要中断，则可通过在gdb中指定文件及代码位置进行断点设置。通过方式1和2，能解决绝大部分的跟踪问题，但是，在运行运行中，我们可能会碰到通过函数指针进行函数调用的情况，此时只知道函数指针的地址，就无法通过函数名或者代码行数进行  
例子：b /src/codefile.cc:81。gdb将在运行到源码文件/src/codefile.cc的第81行中断

方式3、根据运行时的地址设置断点  
此时有两种方式，一是通过直接指定地址进行，进行断点设置。二是通过print命令获得相关信息  
例子1：b *0x5859c0。"*"号是必须加在地址前的，0x5859c0为函数指针的地址  
例子2：展示变量内容  
(gdb) p *thread_scheduler  
$4 = {max_threads = 151, init = 0, init_new_connection_thread = 0x6a3310  
<init_new_connection_handler_thread()>,  
add_connection = 0x5859c0 <create_thread_to_handle_connection(THD*)>,  
thd_wait_begin = 0, thd_wait_end = 0, post_kill_notification = 0,  
end_thread = 0x57ea50 <one_thread_per_connection_end(THD*, bool)>, end = 0}  
在打印thread_scheduler变量的内容时，保存函数指针的变量add_connection的内容被打印出来，保活函数的指针和函数的名字，通过指针可使用b *0x5859c0进行断点设置；通过函数名可使用方式1进行断点设置

[Linux编程基础——GDB（设置断点） - 天方 - 博客园](https://www.cnblogs.com/TianFang/archive/2013/01/20/2868889.html)

启动GDB后，首先就是要设置断点，程序中断后才能调试。在gdb中，断点通常有三种形式：

**断点（BreakPoint）：**

在代码的指定位置中断，这个是我们用得最多的一种。设置断点的命令是break，它通常有如下方式：

- break <function>    在进入指定函数时停住
  
- break <linenum>    在指定行号停住。
  
- break +/-offset    在当前行号的前面或后面的offset行停住。offiset为自然数。
  
- break filename:linenum    在源文件filename的linenum行处停住。
  
- break ... if <condition>    ...可以是上述的参数，condition表示条件，在条件成立时停住。比如在循环境体中，可以设置break if i=100，表示当i为100时停住程序。
  

可以通过info breakpoints [n]命令查看当前断点信息。此外，还有如下几个配套的常用命令：

- delete    删除所有断点
  
- delete breakpoint [n]    删除某个断点
  
- disable breakpoint [n]    禁用某个断点
  
- enable breakpoint [n]    使能某个断点
  

**观察点（WatchPoint）：**

在变量读、写或变化时中断，这类方式常用来定位bug。

- watch <expr>    变量发生变化时中断
  
- rwatch <expr>    变量被读时中断
  
- awatch <expr>     变量值被读或被写时中断
  

可以通过info watchpoints [n]命令查看当前观察点信息

## docker容器和虚拟化的区别

区别：

1、传统虚拟化的创建速度很慢，而容器虚拟化创建速度很快；

2、传统虚拟化增加了系统调节链的环节有性能损耗，而容器虚拟化共性内核，几乎没有性能损耗；

3、传统虚拟化支持多种操作系统，而容器虚拟化仅支持内核所支持的操作系统。

[# docker容器与虚拟机有什么区别？](https://www.zhihu.com/question/48174633)

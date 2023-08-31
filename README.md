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

术语解释：(认为应该List出来的术语解释)
Hypervisor：也称为虚拟机监视器(virtual machine monitor,VMM)，是众多允许多个操作系统(称为guest)在主机上同时运行的虚拟化技术其中一种。
VM：也称Guest OS或者Guest，是可以在Hypervisor中运行的操作系统。 与Host OS对应，其是安装在硬件设备上的系统。
GIC：全称是Generic Interrupt Controller，中文名称通用中断控制器，从外围设备获取中断，确定它们的优先级，并将它们传送到适当的处理器内核。
Passthrough：直通，是关于为给定的guest操作系统提供设备隔离，以便该设备可以由该guest独占使用。
IRQ：为 Interrupt ReQuest的缩写，即中断请求。
vCPU：即电脑中的虚拟处理器，相对于物理CPU而言，vCPU是虚拟机内的CPU。
List Registers：Hypervisor控制接口中的LR寄存器，用来产生虚拟中断。

Terminology: technical terms that should be interpreted with simple words or phrases.
1、	本发明可应用于哪些类型的产品？例如：芯片、芯片模组、终端、基站等。请尽量列举出所有可能。应用于不同类型的产品时， 相应的技术方案是否会有不同，例如被执行的步骤的差异，包含的组件的差异。
What types of products can this invention be applied to?  For example: chips, chip modules, terminals, base stations, etc. Please try to list all the possibilities. For different types of products, will there be any differences, such as the differences in steps to be performed,  the differences in the components included, etc.
芯片/汽车智能座舱

2、	本发明要解决的技术问题是什么？
What technical problems is this invention related to?
当前Hypervisor，在接收硬件中断时，常见的方式为通过相关寄存器判断是哪个VM的中断之后，再分发虚拟中断到对应的VM，这种方式就是用hypervisor接管了硬件中断，再供给上层VM虚拟化中断。
在虚拟化系统中，I/O外设往往只有一套，此时有多个VM需要使用外设，Hypervisor提供了两种方式来实现VM对于硬件外设的访问，分别是passthrough和emulation。当某个硬件设备被配置为passthrough模式时，使得某一VM排他的使用该外设，绕过hypervisor就像将该外设物理连接到所配置VM上一样。这样能够提升性能、降低延迟且可直接利用物理机上的设备驱动，但若有其他VM临时需要获取该外设中信息，则不可能实现，本发明专利即解决上述问题。

3、	本发明的关键点和欲保护点是什么？
What is the key point or the target of this invention?
本发明提出一种在传统中断虚拟化技术中，当某一外设被配置passthrough给某一VM时，若有其余VM想要在后续获取该外设的中断信息，通过GIC能够给其余VM并行发送中断信息的方法。
本发明在上述正常工作的硬件架构中，单独再通过一条通路连接外设及GIC，并在hypervisor中设立一个Arbitrator（中断仲裁器）。当其余VM需要获取外设中断信息时，通过Hypervisor中仲裁器与GIC配合使能外设与GIC之间通路，并通过Hypervisor中的Allocator将中断信息发送到对应VM。

4、	详细介绍技术背景,并描述已有的与本发明最相近似的实现方案及其缺点
Introduce the background information as detailed as possible, and describe the similar art concerning the present invention and the disadvantages thereof)
对于Hypervisor来说，中断响应过程如下图1所示。








图1 Hypervisor中断响应过程
当物理外设产生中断信号时，将信号发送给GIC，GIC内部的Distributor将物理IRQ发送至CPU Interface，此时CPU退出Guest OS返回至Host OS，跳转到Hypervisor模式，并由Host OS驱动响应此中断信号，分配中断向List Register写入Virtual IRQ，再经由Virtual CPU Interface发送至vCPU处理，注入Virtual IRQ到对应Guest OS。
通常的在Hypervisor中的常用方法是使用设备模拟，如下图2所示，在此结构图中，Hypervisor包括各种客户操作系统可以共享的通用设备的仿真，包括虚拟磁盘、虚拟网络适配器等。基于Hypervisor的设备仿真的另一个变体是半虚拟化驱动程序。在这个模型中，Hypervisor包括物理驱动程序，每个客户操作系统都包括一个与管理程序驱动程序协同工作的Hypervisor感知驱动程序（称为半虚拟化或PV驱动程序）。















图2 基于Hypervisor的设备仿真
然而，上述所述共享设备的方法是需要付出代价的，对系统存在额外开销。只要设备需要由多个客户操作系统共享，这种开销是值得的。如果不需要共享，则有更有效的共享设备的方法，即Passthrough，如下图3所示。Passthrough直通是关于为给定的Guest操作系统提供设备隔离，以便该设备可以由该Guest独占使用，这样做的好处有很多，其中最重要的两个就是可以提高性能以及提供对本质上不可共享的设备独占使用。









图3 Hypervisor中的直通
但此时如果有别的VM想要获取已经Passthrough设备的中断信息，由于Passthrough固有的被事先配置的VM独占使用的特性，在实际使用中是无法完成此项任务的。本发明提出的方案即解决上述问题。

5、	本发明技术方案的详细阐述，应该结合流程图、原理框图、电路图、时序图进行说明（可编辑格式的附图）
 Detailed description of the embodiments should be combined with the flow chart, principle figure, circuit diagram, time-sequence diagram， etc.（editable drawings）
对于Hypervisor框架做出基于本发明的修改，优化框架设计如下图4所示。在GIC中新增Interrupt Controller模块，在Hypervisor中新增IRQ Arbitrator、IRQ-Allocator-BE模块，在除配置为Passthrough的VM外的其余VM新增IRQ-Allocator-FE模块。













图4 针对Hypervisor的框架设计
在此架构设计中，物理外设与GIC之间新增Interrupt Controller模块，物理外设有一通路连接至Interrupt Controller模块，此通路在除配置为Passthrough的VM外的其余VM无需获取该物理外设的中断信息时为Disabled状态，当其余VM需要获取时，由Hypervisor控制Interrupt Controller使能此通路，此时中断信息会由此通路，经过Interrupt Controller发送至Hypervisor中的IRQ Arbitrator。所设IRQ Arbitrator功能为接收其余VM需要获取中断信息的请求并记录在VM列表，记录信息包含需要获取的外设编号。所设IRQ Allocator在各个VM中为前端程序，用IRQ Allocator-FE标识，在Hypervisor中为后端程序，用IRQ Allocator-BE标识，IRQ Allocator-FE将各个VM获取物理外设中断信息的需求传递至Hypervisor中的IRQ Allocator-BE，后者再将需求传递至IRQ Arbitrator。
假设系统中现有两个被配置为Passthrough的设备，分别为Device0和Device1，Device0被配置给VM0，Device1被配置给VM1。单独对于Device0，其被VM0排他的使用，当其余VM需要获取其中断信息时，在原有架构中不可能完成。在本专利设计架构中，如下图5所示，每个VM中都设有IRQ Allocator-FE，与Hypervisor中的IRQ Allocator-BE连接，Device0与Device1皆有通路与Interrupt Controller连接。当除VM0外的其余VM如VM1需要获取Device0的中断信息时，工作顺序如下：
1.	由VM通过IRQ Allocator-FE向Hypervisor中的IRQ Allocator-BE发起获取中断信息申请；
2.	IRQ Allocator-BE接收申请后向IRQ Arbitrator注册申请信息，其中包括需要获取信息的Device设备编号以及VM自身编号，放入队列；
3.	IRQ Arbitrator接收请求后，使能Interrupt Controller与对应Device之间通路，中断信息经由此通路再经过GIC发送至IRQ Arbitrator；
4.	IRQ Arbitrator按照队列中记录信息，将Device中断信息通过IRQ Allocator-BE发送至对应VM的IRQ Allocator-FE；
5.	IRQ Allocator-FE接收信息完成后给IRQ Arbitrator发送应答，后者收到应答后关闭Interrupt Controller与Device之间通路，准备下一次工作。
同理对于Device1工作也是如此。
当系统中多其余VM对多Device申请获取中断信息时，如VM2尝试获取Device0、VM3尝试获取Device0、VM2尝试获取Device1的中断信息，则都通过IRQ Allocator发送请求至IRQ Arbitrator，后者将请求按优先顺序放进队列依次处理，并对同Device的请求进行归并，将该Device的中断请求并行发送至多请求VM，实现正常工作。













图5 多VM多Device工作示意图
通过以上系统框架设计，可实现并行发送中断至多VM。

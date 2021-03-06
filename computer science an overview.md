#1. Data Storage

##1.1 Bits and Their Storage
bits: binary digits

###Boolean Operations
The bit 0 represents the value false and the bit 1 represents the value true.
The basic Boolean operations: AND, OR, XOR(exclusive or) and NOT.

###Gates and Flip-Flops
*Gate*: a device that produces the output of a Boolean operation when given the operation's input values is called a gate.
Gates provide the building blocks from which conputers are constructed.
*Flip-flop*: a flip-flop is a circuit that produces an output value of 0 or 1, which remains constant until a pulse(a temporary change to a 1 that returns to 0) from another circuit causes it to shift to the other value. In other words, the output will flip or flop between two values under control of external stimuli.

###Hexadecimal Notation
Stream: a long string of bits.

##1.2 Main Memory
###Memory Organization
*Byte*: a conputer's main memory is organized in manageable units called cells, with a typical cell size being eight bits. a string of eight bits is called a byte.
high-order end/low-order end
most significant bit/least significant bit
*Address*: to identify individual cells in a computer's main memory, each cell is assigned a unique "name", called its address.
Such an addressing system not only gives us a way of uniquely identifying each cell but also associates an order to the cells, giving us phrases such as "the next cell" or "the previous cell".
An important consequence of assigning an order to both the cells in main memory and the bits within each cell is that the entire collection of bits within a computer's main memory is essentially ordered in one long row. Pieces of this long row can therefore be used to store bit patterns that may be longer than the length of a single cell.
**RAM**: Beacuse a computer's main memory is organized as individual, addressable cells, the cells can be accessed independently as required. To reflect the ability to access cells in any order, a computer's main memory is often called random access memory.
DRAM/SDRAM

###Measuring Memory Capacity

##1.3 Mass Storage

###Magnetic Systems
A disk storage system consists of many individual sectors, each of which can be accessed as an independent string of bits.
The location of tracks and sectors is not a permanent part of a disk's physical structure, they are marked magnetically through a process called formatting (or initializing) the disk. 

Evaluate a disk system's performance:
(1) seek time
(2) rotation delay or latency time
(3) access time (the sum of seek time and rotation delay)
(4) transfer rate (in the case of zone-bit recording, the amount of data passing a read/write head in a single disk rotation is greater for tracks in an outer zone than for an inner zone, and therefore the data transfer rate varies depending on the portion of the disk being used.)


#第2章 数据操控
##2.1 计算机体系结构
###CPU(Central Processing Unit)
构成：
1. 算术/逻辑单元（arithmetic/logic unit）
2. 控制单元（control unit）
3. 寄存器单元（register unit）：通用寄存器、专用寄存器

总线（bus）：连接CPU和主存储器
高速缓冲存储器（cache memory）：CPU内部结构，保存主存储器中当前最重要内容部分的副本，可以较快与寄存器进行数据传输。

###存储程序概念（stored-program concept）

##2.2 机器语言
>为了应用存储程序概念，CPU被设计成可以识别二进制模式编码的指令。这组指令以及编码系统统称为机器语言（machine language）。
>使用此语言表达的指令称为机器指令（machine instruction）。

###2.2.1 指令系统
1. RISC（Reduced Instruction Set Computer）
    RISC低耗电，常应用于移动端。
2. CISC（Complex Instruction Set Computer）
CISC代表：英特尔，台式机领域。

机器指令可分为3类：
1. 数据传输类
2. 算术/逻辑类
3. 控制类

####数据传输类：
通常，执行传输指令的过程更像是赋值数据，而不是移动数据。copy或clone能更好描述这组指令。
LOAD：主存储器——填充到——寄存器
STORE：寄存器——填充到——主存储器

#####I/O指令：
与“CPU-主存储器”环境之外的设备通信的指令（打印机、键盘、显示器、磁盘驱动器等）。这些指令处理该机器的输入/输出活动。

####算术/逻辑类：

####控制类：
指导程序执行而非数据操作的指令。

###2.2.2 机器语言的演示
机器指令编码形式包括两部分：操作码（operation code）和操作数（operand）。
操作码字段中的位模式指明该指令要求的是什么基本运算。
操作数字段中的位模式提供操作码指定运算的更详细信息。


##2.3 程序执行
>计算机按需把主存储器的指令复制到CPU中，执行存储器中的程序。
>一旦指令到达CPU，每个指令就会被解码和执行。从存储器中取指令的顺序与这些指令存储在存储器中的顺序相对应，除非被JUMP指令更改。

CPU内部有2个专用寄存器：
1. 指令寄存器（instruction register）。用于存储正在执行的指令。
2. 程序计数器（program counter）。包含下一个待执行指令的地址，用于以机器方式跟踪程序执行到了什么地方。

**机器周期**：取指、译码、执行。
1. 取指：CPU根据程序计数器规定的地址，从存储器中取下一条指令，存入指令寄存器中，然后增加程序计数器的值。
2. 译码：对指令寄存器中的位模式进行译码。
3. 执行：实现指令寄存器里指令所规定的动作。

>**时钟（clock）**：计算机的时钟是一个称为振荡器的电路，生成用于协调计算机活动的脉冲——该振荡器电路生成的脉冲越快，机器周期的执行速度也越快。（不同的CPU设计在一个时钟周期里完成的工作量是不同的，在比较CPU能力是，单纯比较时钟速度意义不大，应采用基准测试）。
>**基准测试（benchmark）**：比较计算机能力。

一旦指令寄存器中的指令执行完毕，CPU又将从取指步骤开始下一个机器周期。

###2.3.1 程序执行示例
###2.3.2 程序与数据
许多程序可以同时存储在计算机的主存储器里，只要它们的地址不同。运行哪个程序可以通过适当地设置程序计数器来决定。

不过，数据也存储在主存储器中，也是用0和1来编码。计算机自己无法知道哪个是程序、哪个是数据。如果程序计数器被赋予的数据的地址而不是程序的地址，那么，CPU会以读取指令的方式读取数据，最终执行结果取决于该数据的位模式。
虽然这种方式感觉会混淆数据和程序，但却也很有用处。因为它使得某一程序可以操控其他程序（包括自身），就像它可以操控数据一样。
设想：一个程序可以根据其与环境的交互自我修正，展现学习能力。或者，一个程序可以编写及执行其他程序，以解决它所遇到的问题。


##2.4 算术/逻辑指令
>算术/逻辑指令组 由算术、逻辑、移位等运算指令组成。

###2.4.1 逻辑运算
>AND、OR、XOR

AND运算的一个主要用途，是将位模式的一部分设为0，而不影响另外的部分。这个应用称为**屏蔽（masking）**，一个称为掩码（mask）的操作数决定另一个操作数的哪个部分会影响结果。
AND运算可以复制一个位串的一部分，方法是在不复制的部分置0。而OR运算也可用于复制一个位串的一部分（在不复制的部分置1）。

XOR运算的一个主要用途，是形成一个位串的反码。将任意一个字节与全部为1的掩码进行XOR运算，可以得到该字节的反码。


###2.4.2 循环移位 及 移位运算
>循环及移位运算用于移动寄存器内的二进制位，常用于解决对齐问题。

移位分类：
以一个字节二进制位的寄存器为例，如果将其内容向右移一位，则最右边的位落到了边界意外，最左端出现了一个空位。对于这个移出的位及留出的空位如何操作，是区别各种移位运算的特征：
1. 循环移位（circular shift或rotation）：将右侧移出的位放置在左端的空位上。
2. 逻辑移位（logical shift）：丢弃移出边界的位，并用0填充空位。
3. 算术移位（arithmetic shift）：保留符号位不变的移位。


###2.4.3 算术运算


##2.5 与其他设备通信
###2.5.1 控制器的作用
计算机与其他设备的通信通常是通过称为控制器（controller）的中间设备来处理。
对于个人计算机，控制器可能由永久安装在主板上的电路组成，或者为了灵活，会采用电路板的形式插入主板的插槽中。

无论哪种形式，控制器都是通过电缆与计算机箱里的外围设备相连、或者与计算机背面的端口（port）相连，其他外围设备可以插到这些端口上。
这些控制器有时候本身就是小型计算机，每个都有自己的存储电路和简单的CPU，可以实现指挥该控制器活动的程序。

控制器将信息和数据来回地在两种形式之间转换：一种是与计算机内部特征相适应的形式，另一种是与所连接外围设备相符的形式。
起初，每种特定类型的外设都有自己的控制器。而现在，通用标准显得更为方便（例如USB通用串行总线）。一个USB控制器可以用作计算机与其他任何同USB兼容的系列设备的接口。

每一个控制器，通过连接到相同的总线完成与计算机的通信（该总线用来连接计算机的CPU和主存）。由于这种连接，每个控制器都能够监控CPU与主存储器之间正在发送的信号，也可以将自己的信号插入总线。

通过这种安排，CPU能够以与主存储器通信的方式与连接在总线上的控制器通信。
为了发送一个位模式给控制器，该位模式首先要在CPU的一个通用寄存器中构建，然后由CPU执行一个类似STORE指令的指令，将该位模式“存储到”控制器中。类似的，当要从一个控制器接收一个位模式时，要使用一条类似LOAD指令的指令。

**存储映射输入输出**（memory-mapped I/O）

###2.5.2 直接内存存取
因为控制器是连接到一台计算机的总线上的，所以它有可能在CPU不使用总线的几纳秒时间里实现与主存储器的通信。
控制器这种存取主存储器的能力称为**DMA（Direct Memory Access）**，可以极大提高计算机的性能。在控制器执行读操作并通过DMA将数据存储在主存储器时，CPU可以继续执行其他任务。于是，这两个活动会被同时执行。CPU将执行某个程序，而控制器则监视磁盘与主存储器之间的数据传输，CPU资源不会被浪费。
使用DMA也会有不利影响，它使计算机总线的通信复杂化。位模式必须在CPU与主存储器之间、CPU与每个控制器之间、以及每个控制器与主存储器之间进行传送。协调总线上的所有这些活动是个很大的设计难题。即使设计非常出色，CPU与控制器竞争总线存取时，中央总线也可能成为障碍。此障碍称为**冯·诺依曼瓶颈（von Neumann bottleneck）**。

###2.5.3 握手
诸如打印未见这样的活动都会包括持续的双向对话，计算机和外围设备之间交换设备状态的信息，协调它们之间的活动。这个活动称为**握手（handshaking）**。
握手通常涉及一个**状态字（status word）**，它是由外围设备生成并发送给控制器的一个位模式。该状态字是一个位图，其中的各个二进制位反映了该设备的各种状态。控制器是自己响应这些状态信息，还是交由CPU处理，这取决于不同的系统。不论哪种情况，状态字都提供了一种机制，用于协调与外围设备的通信。

###2.5.4 流行的通信媒介
>计算设备之间通信有两种途经处理：并行和串行。

**并行通信（parallel communication）**：若干信号同时传输，每个信号都在各自的“线路”上。（数据传输快，但需要相对复杂的通信通路，例如计算机内部总线）。
**串行通信（serial communication）**：一条信号线上，一个信号接一个信号地传输。（只需要一条相对简单的数据路径，因此流行。例如USB通信，网络通信）。

###2.5.5 通信速率
一个计算部件与另外一个计算部件之间传输数据位的速率以bit/s计量。注意，使用缩写形式时，小写英文字母b常表示位（bit），而大写B通常表示字节（byte）。

一个特定设置可获得的最大速率，取决于通信路径的种类以及实现过程中使用的技术。这个最大速率通常大致等同于通信路径的带宽（bandwidth）。不过，该术语除了传输速率，还有容量的含义。即：高带宽意味着通信路径能以高速率传输位，也能够同时携带大量信息。


##2.6 其他体系结构
###2.6.1 流水线
提高执行速度——小型化
改进机器吞吐量（throughput）——流水线技术（pipelining）

###2.6.2 多处理器计算机
**并行处理技术**
**SISD（Single-Instruction stream Single-Data stream, 单指令流单数据流）**
**MIMD（Multiple-Instruction stream Multiple-Data stream, 多指令流多数据流）**
**SIMD（Single-Instruction stream Multiple-Data stream, 单指令流多数据流）**
**多台小型机集成**


#第3章 操作系统
。。。

。。。

##3.3 协调机器的活动
>操作系统如何协调应用软件、实用软件以及操作系统自身内部单元的执行。

###3.3.1 进程的概念
程序与执行程序的活动之间的区别：前者是一组静态的指令；后者是一个动态的活动，其属性会随着事件推进而改变。

**进程（process）**：在操作系统的控制下执行某个程序的活动称为进程。
**进程状态（process）**：与进程联系在一起的活动的当前状态。这个状态包含正在执行的程序的当前位置（程序计数器的值）、CPU中其他寄存器的值以及相关的存储单元。进程状态可以说是机器在特定时刻的快照。

在典型的分时/多任务计算机中，通常会有许多进程同时在执行并竞争计算机资源。
操作系统的任务，就是管理这些进程，使每个进程都能获得其需要的计算机资源（外围设备、主存空间、访问文件以及访问CPU），确保独立进程不会相互干扰，确保需要交换信息的进程能够进行信息交换。

###3.3.2 进程管理
>与协调进程的执行有关的任务，是由操作系统内核中的**调度程序**和**分派程序**处理的。

**调度程序**维护一个有关计算机系统中现存进程的记录（进程池），将新的进程加入到该进程池中，并把已经完成的进程移出进程池。当用户请求执行一个应用时，调度程序就把这个应用加到进程池加以执行。
为了跟踪所有的进程，调度程序在主存中维护着一个信息块，称为**进程表（process table）**。
每当要请求程序执行时，调度程序都在进程表中为该程序创建一个新的表项。这个表项包含例如分配给该进程的存储区（从内存管理程序得到）、进程的优先级以及该进程是出于就绪状态还是等待状态这样的信息。如果进程能够继续执行，那么该进程就处于就绪（ready）状态；如果进程因为要等待某个外部事件的发生而中断，例如海量存储操作的完成、等待键盘的按键以及等待其他进程传来的消息等，那么该进程就处于等待（waiting）状态。

**分派程序**是内核的一个组件，它确保被调度的进程能实际执行。在分时/多任务系统中，这个任务依靠**多道程序设计（multiprogramming）**来完成。即：先将时间划分为小的时间段，每段称为一个时间片（time slice），通常以毫秒或微妙计量，然后把CPU的注意力放在就绪进程上，允许每个进程一次执行一个时间片。这种从一个进程到另一个进程的改变过程，称为进程切换（process switch）或者上下文切换（context switch）。
每当分派程序给进程分配一个时间片，它都会初始化一个计时器电路，通过产生一个**中断（interrupt）**信号来指示时间片的结束。当CPU收到一个中断信号时，它会完成当前的机器周期，保存它在当前进程中的位置，然后就开始执行称为**中断处理程序（interrupt handler）**的程序，该程序存放在主存中预先定义的位置上。中断处理程序是分派程序的一部分，它用来描述分派程序如何响应中断信号。
中断信号的作用是取代当前进程，把控制权传回分派程序。此时，分派程序从进程表的就绪队列（由调度程序决定）中选择优先级最高的进程，重启计时器电路，使被选择的进程开始它的时间片加以执行。
多道程序设计系统能够成功的最大关键，是能够停止进程，并且稍后能重启进程。
重启进程时，必须重新建立的环境就是进程的状态（包括程序计数器的值以及寄存器和相关存储单元的值）。对于为多道程序设计系统开发的CPU，保存这种信息的任务是CPU应对中断信号的工作的一部分。这类CPU还提供机器语言指令，以重新装入先前保存的状态。这种特性简化了分派程序完成进程切换的任务。


##3.4 处理进程间的竞争
操作系统的一个重要任务，是将机器的各种资源分配给系统中的各个进程。
广义上，资源（resource）不仅包括机器的外围设备，还包括机器本身的特性。文件管理程序分配对文件的访问并为新建立的文件分配磁盘空间；内存管理程序分配内存空间；调度程序分配进程表的空间；分派程序分配时间片。

###3.4.1 信号量

以打印机为例，为了控制对打印机的访问，操作系统必须跟踪打印机是否已经被分配。通过使用一个标志（存储在储存器中的一个位），用“置位”标志（set）和“清零”标志（clear）表示打印机是否可用。
但这里有个问题，在操作系统检测到“清零”标志之后、和标志被“置位”之前，这个任务有可能被中断。
（例：如果打印机当前可用，一个进程请求它的使用权，操作系统检测到标志清零，表明打印机可用，然后这个进程被中断。而另一个进程也请求打印机的使用，检测标志依然清零，操作系统允许第二个进程使用打印机，而随后第一个进程恢复执行，由于中断前已经检测过打印机可用，系统会允许第一个进程也是用打印机。由此造成冲突。）

**解决办法**：测试和标志置位任务必须在无中断的条件下完成。
1. **中断屏蔽指令+中断允许指令**。用中断屏蔽指令开始一个标志测试，在测试和置位任务完成后，以中断允许指令结束。
2. 使用**测试并置位（test-and-set）**指令，确保测试和置位在同一条机器指令内完成，不会出现中断问题。

**信号量（semaphore）**：代指上文中可以正确运作的标志。
当一段指令一次只能被一个进程执行时，称之为**临界区（critical region）**。一个临界区一次只允许被一个进程执行，这个要求叫做**互斥（mutual exclusion）**。
*获得对一个临界区的互斥，常用办法就是用一个信号量守护这个临界区。*
一个进程要进这个临界区，必须确定这个信号量是清零的，并在进入临界区之前把它置位，然后在出临界区时把这个信号量清零。如果发现这个信号量在置位状态，那么试图进入临界区的进程必须等待，直到这个信号量被清零。

###3.4.2 死锁
死锁状态下，两个或更多的进程被阻塞，不能执行，因为它们中的每一个都在等待已经分配给另一个的资源。

当下述三个条件都具备时，就可能出现死锁：
1. 存在对不可共享资源的竞争；
2. 这些资源是在不完整的基础上请求的。也就是说，一个进程接受了某些资源后，稍后还将请求其他的资源。
3. 一个资源一旦被分配出去，就不能以强制的办法再回收。

一般来说，只要抑制其中一个条件，就可以避免死锁。

- 抑制第三个条件的技术：属于死锁检测和改正方案的范畴。（只在死锁出现的时候检测出它，然后通过强制性回收某些已经分配出去的资源来改正它。建议在死锁很少可能出现的情况下使用这种方案。）
- 抑制前两个条件的技术：称为死锁避免方案。
    + 针对第二个条件：要求每个进程一次性地请求它所需要的全部资源。
    + 针对第一个条件：将不可共享的资源转变为可共享的资源。（例如，当同时有多个打印请求时，操作系统建立多个虚构打印机，将要打印的信息先临时存储在海量存储器上，等到打印机可用时，逐一加载这些请求。这种保存数据供以后再合适的时候输出的技术，称为**假脱机（spooling）**）。
假脱机，是一个允许多个进程访问一个公共资源的技术，可以有多种变体（例如文件管理程序可以批准若干个进程访问同一个文件，前提是它们只读取数据。）


##3.5 安全性
>安全性有多种表现形式，可靠性就是其中一种。

###3.5.1 来自机器外部的攻击
操作系统的一个重要任务：保护计算机的资源，防止受到非授权用户的访问。

**审计软件（auditing software）**
**嗅探软件（sniffing software）**

计算机系统安全领域中的主要难题之一，就是用户自己的不小心。

###3.5.2 来自机器内部的攻击
当入侵者以普通账号访问时，会试图欺骗操作系统，以获得未授予的权限。例如，尝试欺骗内存管理程序，让一个进程访问其被分配的存储区之外的内存区域；或者欺骗文件管理程序，访问本来无权访问的文件。

关于上面的跨内存问题，需要通过内存管理程序，将进程限制在给它分配的内存区域内。如果没有这种限制，一个进程就能够从内存中覆盖掉操作系统，从而接管对计算机的控制。
解决方案：为多道程序设计系统设计的CPU，通常包括若干个专用寄存器，操作系统可以在这些寄存器中保存分配给一个进程的储存区域的上下界。当执行该进程时，CPU把每个存储器引用与这些寄存器中的值进行比较，以保证该引用在指定的界限之内。如果发现这个引用在为该进程指定的区域之外，CPU将自动把控制权交还给操作系统（借助中断处理），这样操作系统可以做出合理的处理。

但这个解决方案有漏洞，如果没有进一步的安全措施，一个进程只要改变含有存储区界限的专用寄存器的值，就可以访问指定区域以外的内存区域。

为了防止这种恶意活动，将多道程序设计系统的CPU设计为工作在两种**特权级（privilege level）**之一的模式下。（有特权模式和无特权模式）
当处于有特权模式下，CPU能接受自己的机器语言可处理的所有指令；当处于无特权模式下，CPU能接受的指令是有限的。
仅在有特权模式下才能执行的指令，称为**特权指令（privileged instruction）**。（典型的特权指令例：改变内存界限寄存器内容的指令和改变CPU当前特权模式的指令。）
当CPU处于无特权模式时，任何执行特权指令的企图都将引起中断。这个中断将CPU转变为有特权模式，并将控制权交给操作系统内部的中断处理程序。
刚开机时，CPU处于有特权模式，因此操作系统在引导过程后开始启动时，所有的指令都可以执行。然而，每当操作系统允许一个进程开始执行它的时间片时，就通过执行“改变特权模式”的指令，将CPU切换到无特权模式。于是，如果一个进程试图执行有特权指令，操作系统就会得到通知，这样操作系统就充当了维护计算机系统完整性的角色。


#第4章 组网及因特网

##4.1网络基础
###4.1.1 网络分类
计算机网络通常分为：

- LAN(Local Area Network，局域网)
- MAN(Metropolitan Area Network，城域网)
- WAN(Wide Area Network，广域网)

基于公共领域还是特定实体控制的分类：

- 开放式网络（open）
- 封闭式网络（closed），也称专用网络（proprietary）

基于网络拓扑学（连接模式）的分类：

- 总线型拓扑：所有计算机通过同一条称为“总线”的通信线路连接起来。（例：以太网）
- 星型拓扑：将一台计算机作为中心，所有其他计算机都与之相连。（中央计算机称为AP（Access Point））

总线型和星型的区别在于，网络中的计算机是通过一条公共总线直接相互通信，还是通过中央计算机媒介间接通信。

###4.1.2 协议（protocol）

- 基于以太网标准的总线型网络中，报文传输的许可是通过名为**CSMA/CD**的网络协议控制的。
>CSMA/CD: Carrier Sence, Multi-Access with Collision Detection, 带冲突检测的载波侦听多路访问

    CSMA/CD网络协议规定，每条报文都要广播给总线上的所有计算机，每台计算机都对所有报文进行监听，但只保存发送给自己的报文。为了传输报文，计算机需要等到总线处于空闲状态，才开始传输报文并继续监听总线。如果另一台计算机也开始传输报文，那么两台计算机都会检测到冲突，并各自暂停随机长的一小段时间，然后再次尝试。

- 在无线星型网络中，所有计算机都通过中央接入点通信，原因在于一台计算机可能无法检测到与其他计算机的传输冲突（例如信号淹没、隐藏终端问题等）。这使得无线网络采用避免传输冲突的方法，而不是检测冲突的方法。这类方法被归类为**CSMA/CA**。
>CSMA/CA: Carrier Sence, Multiple Access with Collision Avoidance, 带冲突避免的载波侦听多路访问

    冲突避免协议的设计目的是避免冲突，也许并不能完全消除冲突。当冲突发生时，必须重新传输消息。
    冲突避免的常见方法：P101。（此处有待理解）


###4.1.3 网络互连
>有时，需要连接现存的网络以形成一个扩展的通信系统，形成相同类型的更大网络。

对于同样基于以太网协议的总线型网络，可以将总线连接起来形成一个长总线。可利用中继器、网桥、交换机等设备完成。整个系统会像每个初始的小网络一样，用相同的方式运作。

-   **中继器（repeater）**：最简单，仅在两个原始总线间来回传送信号。
-   **网桥（bridge）**：也是连接两条总线，但不必在线路上传输所有报文。网桥会检查每条报文的目的地址，当该报文目的地是另一边的计算机时才将其在线路上传输。因此，网桥同一侧的两台计算机通信时不需要打扰另一边的计算机，更加高效。
-   **交换机（switch）**：本质上就是具有多连接的网桥，可以连接若干条总线，不止两条。被转发的报文只会送至相应的“辐条”，因此减轻了每根“辐条”的传输流量。

然而，要连接的网络有时会有不兼容的特性。例如WiFi网络的特性就可能与以太网网络中的不兼容。

这种情况下，网络需要通过建立一个**互联网（internet）**方式连接。在这个网络中，原始的网络仍然保持其独立性，并且继续作为独立的网络运行。

>这里的互联网（internet）不等同于因特网（Internet），后者代指一种独特的、世界范围的互联网。

把网络连接起来形成互联网的设备是**路由器（router）**，这是一种用来传送报文的专用计算机。
路由器的任务与中继器、网桥和交换机不同，路由器提供了网络之间的链接，并允许每个网络保持它独特的内部特性。

路由器可以向适当的方向转发报文，这个转发过程基于互联网范围的寻址系统。其中互联网上的所有设备（包括原始网络中的计算机和路由器）都被赋予了唯一的地址。（这样，原始网络中的每台计算机都有两个地址：自己网络内的“本地地址”和它的互联网地址）。

一台计算机想给远程网络中的另一台计算机发送报文，就要附上报文目的地的互联网地址，然后把报文发送给其本地的路由器，路由器将把报文向正确的方向转发。为了转发报文，每个路由器都维护了一张**转发表（forwarding table）**，该表中包含了根据目的地地址消息应该发送的方向这种路由信息。

一个网络与互联网链接的“点”经常称为**网关（gateway）**，因为它是网络与外部世界之间的通道。网关有多种形式，有时网关指的是路由器，有时可能不限于此。

###4.1.4 进程间通信的方法
**进程间通信（interprocess communication）**：一个网络中，在不同计算机上执行（以及一台计算机上通过分时/多任务处理执行）的各种活动（或进程）必须经常互相通信，以便协调行动并完成指派的任务。

进程间通信通常采用**客户机/服务器（client/server）**模型。这种模型规定了进程的基本角色：1. 向其他进程发出请求的client、2. 满足client请求的server。

客户机/服务器模型不是进程间通信的唯一方式，另外一种是**对等模型（peer-to-peer，简称P2P）**。

###4.1.5 分布式系统（distributed system）

####集群计算（cluster computing）
与超级计算机相比，成本低、可靠性高、维护成本也更低。

- **高可用性（high-availability）**：更好保证集群中至少有一台计算机可以响应请求，即使集群中其他计算机发生故障或不可用。
- **负载平衡（load-balancing）**：负载可以自动从集群中负载太大的计算机转移到负载很小的计算机上。

####网格计算（grid computing）
一种分布式系统，安装在用于其他目的的计算机上，当机器空闲时便可为网格自愿提供计算能力。

####云计算（cloud computing）
凭借**云计算**，网络上大量的共享计算机得以被按需分配给客户机使用。云计算是分布式系统中的最新趋势。因特网使得实体可以将其数据和计算委托给“云”，这里的“云”指的是网络上可用的大量计算资源。


##4.2 因特网（Internet）
###4.2.1 因特网体系结构
ISP：Internet Service Provider，因特网服务提供商。负责网络的构建和维护。

因特网的构成：

1. 第一层ISP
2. 第二层ISP
3. 因特网接入服务提供商（access ISP）
4. 终端系统

>第一层和第二层因特网服务提供商本质上是路由器的网络，集中提供因特网通信基础设施（因特网的核心）。然后通常由因特网接入服务提供商来提供与这一核心的接入服务。因特网接入服务提供商本质上是独立的互联网，有时也称为内联网（intranet）。

>终端系统与因特网接入服务提供商连接的技术也不尽相同。例如，发展对快的WiFi技术无线连接，是将接入点与因特网接入服务提供商相连接，因此接入点的广播范围内，都可以通过因特网接入服务提供商向终端系统提供因特网接入。接入点范围内的区域称为**热点（hot spot）**。

**调制解调器（modem）**：将数字数据转换为与使用传输媒介兼容的格式。
例如**DSL**把低于四千赫兹的频率范围用来满足传统语音通信，更高的频率用于传输数字数据。
>DSL：Digital Subscriber Line，数字用户线路


###4.2.2 因特网编址

###4.2.3 因特网应用


##4.3 万维网（World Wide Web）
###4.3.1 万维网实现
>超文本、超链接、超媒体

用于上网的两种软件包：浏览器（browser）软件包——服务器（Web server）软件包

超文本通常使用**HTTP**的协议在浏览器与万维网服务器之间传输。
>HTTP：Hypertext Transfer Protocol，超文本传输协议

为了在万维网上定位及检索文档，每个文档都被赋予了唯一的一个地址，称为**URL**。
>URL: Uniform Resource Locator，统一资源定位符。

每个URL都包含浏览器要连接到的正确服务器以及请求希望的文档所需要的信息。

URL可以包含四段（不一定全有）：
    1. 与服务器之间的通信协议
    2. 服务器所在机器的助记地址
    3. 目录路径
    4. 文档名

>**W3C**：World Wide Web Consortium，万维网联盟。宗旨是开发协议标准（W3C标准）来促进万维网的发展。

###4.3.2 HTML
Hypertext Markup Language
###4.3.3 XML
###4.3.4 客户端和服务器端的活动
请求网页的简单步骤：

1. 客户端浏览器使用URL信息，与控制该网页的服务器建立连接。
2. 客户端请求服务器传回该页的一个副本。
3. 服务器将请求的文档传给客户端。
4. 浏览器解析该文档，展示为网页。

不过，如果我们想获得一个带有动画的网页，或者允许客户填写订单并提交的网页，这些需求需要浏览器或服务器付出额外的行动。


##4.4 因特网协议
>报文如何在因特网上传输。
>因为传输过程需要系统中所有计算机合作，所以控制传输过程的软件需要驻留在因特网的每台计算机中。

###4.4.1 因特网软件的分层方法
网络软件的首要任务——提供从一台机器到另一台机器传输报文所需的基础设施。
在因特网上，报文传递活动是通过软件单元的层次结构完成的。软件总共有四层：

1. 应用层（application layer）
2. 传输层（transport layer）
3. 网络层（network layer）
4. 链路层（link layer）

简单来说：由应用层产生一个报文，向下传递，经由传输层和网络层，最后传递到链路层进行传输。目的地的链路层接收这条报文，沿逆向分层结构向上传递，直到交给应用层。

详细：

1. **应用层**：由使用因特网通信来完成任务的软件单元组成。（例如客户机和服务器软件，还包括FTP协议传输软件、利用SSH提供远程登录的软件等）。应用层在向传输层发送或接收报文时，需要向因特网基础设施提供兼容的地址，因此应用层需要利用因特网上的域名服务器提供的服务，将域名地址翻译成IP地址。
2. **传输层**：从应用层接收报文，并确保报文以正确的格式在因特网上传输。为了第二个目的，传输层将长报文分成小的片段作为独立单位在因特网上传输。因为在因特网内，一个长报文会阻塞许多报文必经的节点，所有需要对长报文分段。（小段报文在这些节点可以交叉通过，而长报文在经过这些节点时将迫使其他报文等待。）传输层在生成的小片段上增加序列号，然后将这些称为**分组（packet）**的片段交给网络层。从这一刻起，这些分组被认为是彼此独立而无关的报文，直到它们到达最终目的地的传输层。这些同属于一个长报文的分组，很可能沿着不同的路径在因特网中传输。（这些片段可以在报文的目的地重新组合）
3. **网络层**：网络层的任务是在因特网传输路径的每个步骤上，决定分组的下一个发送方向。
    网络层和其下层的链路层的组合构成了驻留在因特网路由器上的软件。网络层负责维护路由器的转发表，并使用此表决定分组的转发方向。路由器中的链路层负责接收和传输分组。
    当分组发源地的网络层接受来自传输层的分组时，它使用其转发表来决定分组应该被发送到哪里，并在那里开始分组的旅程。决定好合适的方向后，网络层把分组交给链路层，进行实际传输。
4. **链路层**：传输和接收分组。链路层必须要处理目的计算机所在的个体网络独特有的通信细节。例如，如果网络是以太网，链路层将使用CSMA/CD协议；如果网络是WiFi网，链路层将使用CSMA/CA协议。
    当分组被传输后，它被处在连接另一端的链路层接收到。在那里链路层把分组向上交给网络层，由网络层把分组的最终目的地和网络层的转发表进行比对，决定分组下一步的方向。当做出这个决定后，网络层把分组返回给链路层，分组沿着它的路径被转发。使用这样的方式，分组从一台机器跳到另一台机器，最终到达它的目的地。

在这个旅程中，只涉及中转站的链路层和网络层，路由器上只有这两个层。为了减少在每个中转站上的延迟时间，路由器中的网络层转发角色紧密地与链路层集成在一起。由此，现代路由器转发一个分组所需的时间用微秒来衡量。

在分组的最终目的地，由网络层来确认分组的旅程已经完成。然后，网络层把分组交给它的传输层，而不再转发它。传输层从网络层接收这个分组时，它提取组成报文的基本片段，并按照报文源端传输层所提供的片段序列号重组原始的报文。一旦报文重组完成，传输层就把它交给应用层的适当单元——报文传输过程完成。

确定应用层内哪个单元来接收到来的报文，是传输层的一个重要任务。每个单元被分配了唯一的端口号（port number）。传输层在报文开始传输旅程之前，要把适当的端口号附加到报文地址上。然后，一旦目的地的传输层收到报文，它只需将报文交给指定端口号上的应用层软件。
（用户很少需要关心端口号，因为对于普通的应用，有通用的端口号。例如，如果通过万维网检索某个URL资源，浏览器一般会通过80端口与该域名下的HTTP服务器联系；当传输文件时，FTP客户机认为应当通过20和21端口与FTP服务器通信。）


###4.4.2 TCP/IP协议簇


#第5章 算法


#第6章 程序设计语言

 
#第7章 软件工程
>软件工程，致力于寻找指导大型复杂软件系统的开发原则。
##7.1 软件工程学科
>可靠性是最主要的问题。

**CASE（Computer-Aided Software Engineering, 计算机辅助软件工程）** 的出现，使软件开发流程化，简化了软件的开发过程。

**CASE工具**：

1. 项目设计系统
2. 项目管理系统
3. 文档工具
4. 原型与仿真系统
5. 界面设计系统
6. 编程系统

**IDE（Integrated Development Environment，集成开发环境）**


##7.2 软件生命周期
>软件工程最基础的概念，就是软件生命周期。

    开发——>使用<——>维护

软件一旦开发完成，就进入一个既被使用又被维护的循环，直至软件生命周期结束。

>维护软件可能是一个非常严峻的工程。


###7.2.2 传统开发阶段
主要步骤：

1. 需求分析
2. 设计
3. 实现
4. 测试



#第8章 数据抽象
>本章研究如何对数据组织形式进行模拟，称为数据结构。目标是让数据的使用者将数据集视为一种抽象的工具来访问。

##8.1 数据结构基础

###8.1.1 数组
1. **同构数组（homogeneous array）**：一种“矩形”数据块，其项具有相同的类型。
2. **异构数组（heterogeneous array）**：是一种可能具有不同类型项的数据块。块里的项通常称为**部件（component）**。

###8.1.2 列表、栈和队列
**列表（list）**：一组数据，其表项按顺序排列，其开头称为**表头（head）**，尾端称为**表尾（tail）**。

几乎所有的数据集合都可以看成列表。
通过严格限制列表中项的访问方式，我们可以得到两种特殊类型的表，称为栈和队列。

**栈（stack）**：该表的项只能在表头进行添加和删除。栈的头称为**栈顶（top）**，栈的尾称为**栈底（bottom或base）**。在栈顶增加新项称为**入栈（pushing）**，在栈顶删除一项称为**出栈（popping）**。最后入栈的数据最先出栈，是**LIFO**结构。

对于那些检索次序与存储次序相反的存储数据项而言，这种后进先出特性意味着栈是理想的选择，所以栈经常被用作回溯活动的基础。（回溯，backtracking，指退出系统的过程与进入系统的次序相反）。

**队列（queue）**，是这样的一种列表，其表项只能从表头删除，新表项只能从表尾插入。队列是**FIFO**的结构。队列常被用作缓冲区的基本结构。

###8.1.3 树
**树（tree）**，一种数据集合，其项具有层次化的组织形式。

树中的每一个位置称为一个节点（node）；





#第9章 数据库系统



#第10章 计算机图形学



#第11章 人工智能

#第12章 计算理论
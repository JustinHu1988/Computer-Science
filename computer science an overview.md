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

- 在无线星型网络中，所有计算机都通过中央接入点通信，
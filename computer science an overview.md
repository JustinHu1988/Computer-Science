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

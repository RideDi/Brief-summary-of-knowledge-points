# JVM Memory & GC

GC区别C++，C++不含GC，要自己实现

## JVM 内存管理

JVM将内存化为几个区域

```
1.方法区	Method Area
2.堆区	Heap
3.虚拟机栈	VM Stack
4.本地方法栈	Native Method Stack
5.程序计数器	Program Counter Register
```

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctNzFmZjkwYjA3OTQ4ZmUyZS5wbmc?x-oss-process=image/format,png)

方法区和堆 所有线程共享

### 方法区

存放需要加载的类的信息(类名、修饰符)、静态变量、构造函数、final定义的常量、类中的字段和方法信息。全局共享， 一定条件会GC，超出大小时会OutOfMemory:PermGen Space

运行时常亮池 是方法区的一部分，存储编译器生成的常量和引用。

### 堆区Heap

是GC最频繁的，由所有线程共享，在虚拟机启动时创建，主要存放对象实例及数组，所有new出来的对象都储存在这个区域

### 虚拟机栈

占用OS 内存，每个线程对应一个虚拟机栈，线程私有。生命周期和线程一样，每个方法执行时产生一个栈帧Stack Frame存储局部变量动态链接、操作数和方法出口等信息，方法被调用时，栈帧入栈，方法调用结束时栈帧出栈。



局部变量表中存储着方法相关等布局变量，包括各种基本数据类型及对象的引用地址。因此有个特点：**内存空间可以在编译期间就确定，运行时不再改变**。

VM Stack定义了两种异常： **StackOverFlowError(栈溢出)** 和 **OutOfMemoryError(内存溢出)**如果线程调用的栈深度大于虚拟机允许的最大深度，则抛出StackOverFlowError；不过大多数虚拟机都允许动态扩展虚拟机栈的大小，所以线程可以一直申请栈，直到内存不足时，抛出OutOfMemoryError。

本地方法栈

支持native方法执行，储存了每个native方法的执行状态，和虚拟机栈运行机制一样，唯一区别是**虚拟机栈执行java方法，本地方法栈执行native方法**

### 程序计数器PCR

是一个很小的内存区域，不在RAM上，直接划分在CPU上，程序员无法操作，作用是：**JVM在解释.class字节码文件时，储存当前线程执行的字节行行号(各JVM方式不同)**字节码解释器工作时，通过改变PCR的值来取下一条要执行的指令，分支、循环、跳转等基础功能都是靠PCR

每个PCR只能记录一个线程等行号，因此是线程私有的。

如果当前正在执行的是JAVA方法，则PCR记录的是正在执行的虚拟机字节码指令的地址。如果执行的是native方法，计数器值为空，此内存区是唯一不会抛出OutOfMemoryError的区域



## GC机制

随着程序的运行，内存中的实例对象、变量等占据的内存越来越多，如果不回收，会降低程序运行效率，甚至引发异常



上面五个区域中，有三个不需要GC：本地方法栈、PCR、虚拟机栈，因为生命周期和线程同步，线程销毁就会自动释放其占有的内存。**只有方法区和堆区需要GC**



### 查找算法

经典的引用计数器法，每个对象添加到引用计数器，引用一次+1，失去引用-1，在一段时间为0时就认为可以回收。-->缺点：两个没用的对象互相引用，不符合条件。

⬇️

根搜索算法

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctOTk4ZmVkNzdhNzYxMmUxYi5wbmc?x-oss-process=image/format,png)

从GC Roots节点出发，向下搜索，如果一个对象无法到达GC Roots的时候就说明不在引用，可以被回收。



Def:(>JDK1.2)

- 强引用：new出来的对象都是强引GC不会回收，甚至可以抛出OOM
- 软引用：JVM内存不足时才会回收
- 弱引用：只要GC立刻回收，不论内存充足与否
- 虚引用：跟踪记录，辅助finalize函数

```
需要被回收的类
1.该类的所有实例都被回收
2.加载该类的ClassLoad已经被回收
3.该类对应的反射类java.lang.Class对象没有被任何地方引用
```



### 内存分区

​		JVM在程序运行过程当中，会创建大量的对象，这些对象，大部分是短周期的对象，小部分是长周期的对象，对于短周期的对象，需要频繁地进行垃圾回收以保证无用对象尽早被释放掉，对于长周期对象，则不需要频率垃圾回收以确保无谓地垃圾扫描检测。为解决这种矛盾，Sun JVM的内存管理采用分代的策略。

**新生代、旧生代、持久代**

采用不同GC算法

新生代	--->	生命周期短、快速创建销毁的

旧生代	--->	生命周期较长的对象

持久代	--->	在Sun HotPot虚拟机中指方法区(部分JVM没有持久代)

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctZDY0NzA2NTliZDExNmQwYy5wbmc?x-oss-process=image/format,png)

新生代	--->	分为Eden区 和 Survivor区

​						  Survivor区分为大小相同的FromSpace和ToSpace

​						  新建对象从新生代分配内存，Eden不足就把存活对象转移到Survivor区，进行GC时会发出Minor GC(Youn GC)

旧生代	--->	存放新生代多次回收依旧存活的对象(Eg:缓存)旧生代满了就对其进行GC称作 Major GC(Full GC)

持久代	--->	在Sun HotPot虚拟机中指方法区(部分JVM没有持久代)



### GC算法

常见的GC算法：**复制、标记-清除和标记-压缩**

**复制**：从根集合开始扫描，将存活的对象移动到空间区域

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctMGY0MDk0NDEzOTZlOTFmZC5wbmc?x-oss-process=image/format,png)

存活对象少的时候比较高效(新生代Eden采用复制)需要额外的空间和对象移动

**标记-清除**：从根集合开始扫描，对存活的标记，标记后再扫描整个空间中未标记的进行清除。

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctNmNjMmRkMjg0ZGUyODg4YS5wbmc?x-oss-process=image/format,png)

在Marking阶段需要全盘扫描，耗时，不需要移动对象，且不对存活的进行整理，空间中对象多的时候，效率高，但是会有内存碎片

**标记-压缩**：与上述类似，先扫描标记，然后扫描清除，但是清除后会把存活的对象向左空闲空间进行压缩，然后更新指针。

![image.png](https://imgconvert.csdnimg.cn/aHR0cDovL3VwbG9hZC1pbWFnZXMuamlhbnNodS5pby91cGxvYWRfaW1hZ2VzLzIwMzIxNzctOWRlNTM4Mzg2ZTdjODk0Ny5wbmc?x-oss-process=image/format,png)

避免了内存碎片，但是有移动成本。(适用于旧生代)

## 垃圾收集器

JVM中，GC由垃圾回收器来执行，需要选择合适的垃圾收集器

- 串行收集器(Serial GC)

  ​	最古老且基本的收集器，现在依旧广泛使用，JAVA SE5和JAVA SE6中客户端虚拟机采用的默认配置。适合只有一个处理器的系统。串行处理器中minor 和 major GC过程都是采用一个线程进行回收的，
  ​	**进行GC时，需要对所有正在执行的线程暂停(stop the world)**如果实时性要求不高，收集器适用于单CPU、新生代空间较小且对暂停时间要求不高的应用上，是client级别的默认GC

- PaeNew GC

  ​	基本和Serial GC一样，本质区别加入了多线程，提高效率，可以用于server 同时可以和CMS GC配合。

- Parallel Scavenge GC

  ​	扫描和复制过程采用多线程的方式，适用于多CPU、对暂停要求短的应用，server级别的默认GC

- CMS(Concurrent Mark Sweep)收集器

  ​	收集器的目的是解决Serial GC停顿的问题，达到最短的回收时间。常见B/S架构的应用就适合这类收集器。因为其高并发、高响应，CMS基于标记-清除实现。

  - 优点：并发收集、低停顿
  - 缺点：
    - CMS对CPU资源敏感，并发阶段不会导致用户停顿，但是会占用CPU导致程序变慢，总吞吐量下降
    - CMS收集器无法处理浮动垃圾，可能出现"Concurrent Mode Failure" 失败导致另一次Full GC
    - CMS收集器基于标记-清除，产生碎片

- G1收集器

  ​	相比CMS收集器有不少改进，基于标记-压缩，不会产生碎片，精确控制停顿

- Serial Old收集器

  ​	是Serial收集器的老版本，单线程收集，使用标记-整理算法主要在Client下的虚拟机

- Parallel Old 收集器

  ​	Parallel Scavenge 收集器的老年代版本，使用多线程，标记-整理

- RTSJ 收集器

  ​	用于Java实时编程














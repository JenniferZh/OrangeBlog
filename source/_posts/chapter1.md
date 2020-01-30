---
title: 程序员的自我修养——操作系统回顾
date: 2020-01-30 14:18:29
tags: 
- reading
- 程序员的自我修养
---

本文回顾了一些操作系统的常识

## 计算机硬件

1. 计算机的三个最重要设备

- **CPU**
    - 分类
        - SMP: 多CPU
        - Multicore: 多核心，核心之间共享昂贵的缓存部件
    - 指令集
        - x86
        - MIPS 嵌入式
    - x86 平台有65536个硬件端口寄存器

- **MEMORY**

- **I/O控制芯片**

2. 设备的连接 - **总线**
- PCI总线，北桥，高速，链接 CPU,MEMORY,CACHE
- ISA总线，南桥，低速，链接 USB,DISK

## 系统软件
> Any problem in computer science can be solved by another layer of indirection

1. 分类
- 平台性： OS内核，驱动程序，运行库，系统工具
- 程序开发：编译器，连接器，汇编器

2. 结构
![](/images/architect.jpg)

## 操作系统

1. 定义
操作系统的一个功能是提供抽象接口，一个功能是管理硬件资源

2. 操作系统如何让硬件物尽其用
    - CPU：不要让CPU打盹
        - multi task 多道程序
        - time sharing 分时复用
    - 其他硬件：硬件抽象管理
        - 图形：GDI
        - 声音多媒体：DirectX
        - 磁盘：文件系统
    - 内存：内存不够怎么办？ **分页**
        - 虚拟地址空间，每个进程有自己的虚拟地址空间，虚拟页(Virtual Page)
        - 真实地址空间，计算机只有一份-对应真实内存，物理页(Physical Page)/磁盘页(Disk Page)
        - **MMU**：一般集成在CPU里，用来转化虚拟地址为真实地址
        - **Page Fault**：当访问到的虚拟页在内存中找不到对应的物理页，就会产生中断把这一页换入内存

## 线程
1. 定义
    - 线程：程序执行的最小单元
    - 进程：A process is an instance of a program running in a computer

2. 组成
    - 线程私有：线程ID+当前指令指针+寄存器+堆栈+TLS
    - 线程共有：code, data, 进程空间，打开文件

3. 线程调度
![](/images/thread.jpg)

4. 饿死(Starvation)
    - 定义：线程的优先级永远很低，无法进入running状态
    - 如果一个CPU密集型线程得到了高优先级，容易造成其他线程饿死；如果一个IO密集型线程得到了高优先级，不容易造成其他线程饿死。因为IO密集型线程容易自己让出CPU，而CPU密集型等时间片用尽才会让出CPU。


---
title: OS - 虚拟存储
categories: [CS base]
tags: [OS]
---

OS复习过程中，关于虚拟存储部分的简单笔记，描述未必准确，只是帮助自己理解。



### 覆盖和交换

#### 覆盖

将程序分成若干个功能相对独立的模块，将没有调用关系的模块分成一组放入同一个共享内存区域。
1. 必要部分：主要功能常驻内存
2. 可选部分：不常用功能，需要时装入内存
3. 没有调用关系的模块必要时可以相互覆盖
4. 缺点：
    - 增加运行时间
    - 增加编程难度

<!-- more -->

#### 交换

增加正在运行的进程的内存空间
1. 暂时不能运行的的进程丢进外存（挂起）
2. 换入换出的基本单位：`整个进程`的地址空间
3. 几个问题：
    - 何时交换：内存不够/有不够的可能时
    - 交换区大小：能存放所有用户进程的所有镜像的拷贝
    - 程序换入时的重定位：动态地址映射的方法


#### 覆盖&交换比较

> 覆盖：（程序员）
    >  - 进程无关的模块之间
    >  - 需要知道模块之间的逻辑关系
    >  - 发生在程序内部模块间
>
> 交换：（OS）
    > - 以进程为单位
    > - 不需要知道模块之间的逻辑关系
    > - 发生在内存进程间


### 局部性原理

- 时间局部性：多次执行/访问集中在较短的周期
- 空间局部性：当前指令/数据和相邻指令/数据集中在较小的区域中
- 分支局部性：多次跳转可能跳到相同位置（循环）


### 虚拟存储的概念
- 思路：不常用的部分内存块丢到外存中
- 原理：
    - 程序装载时：将当前需要的页或段装入内存
    - 执行中：缺页或缺段时，OS将相应页/段调入内存
    - OS将内存中暂时不用的页面/段保存到外存（页面置换算法）
- 实现方式：
    - 虚拟页式存储
    - 虚拟段式存储
- 基本特征：
    - 不连续性
    - 大用户空间
- 支持技术
    - 硬件 - 地址转换机制
    - OS - 管理换入换出


### 虚拟页式存储
- 思路：部分页面装入内存
- 和页式存储的区别：
    - 页式存储所有页面均在内存（不存在缺页异常）
    - 虚拟页式存储添加请求调页和缺页处理
- 页表项结构添加的标志位
    - 访问位：该页面是否被访问过
    - 修改位：内存中的该页是否被修改
    - 保护位：读写执行权限
    - 驻留位：页面是否在内存（1:在）

















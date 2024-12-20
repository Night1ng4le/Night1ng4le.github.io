---
title: 《一些证明自己很菜的错题记录I》
categories: [Leetcode]
tags: [Coding,Array,Note,Data Structure]
---

有种当年学c++刷题库的感觉。所有错误答案分析来自于某论坛。

<!--more-->

> 1. 数组的地址计算与存储方式无关。 
> **False**

**Reason:**因为数组的存储方式可以分为行优先和列优先，地址计算是有差别的。


> 2. 数组Ｑ［0..m-1］用来表示一个循环队列， 用front指向队头元素，rear指向队尾元素的后一个位置 ，则当前队列中的元素数是。（队列总的元素数不会超过队列大小）
> A. (rear-front+m)% m
> B. rear-front+1
> C. rear-front-1
> D. rear-front
> **A**

**Reason:** 因为是循环链表 rear不一定就比front地址高 所以有可能rear-fornt得到结果是负数 所以为了正确性起见需要+m再%m

> 3. JDK8及其以后版本，HashMap的数据结构是数组+链表+红黑树。 
**True**

> 4. (多选)下列叙述哪些是对的?
> A. 线性表的逻辑顺序与物理顺序总是一致的。
> B. 线性表的顺序存储表示优于链式存储表示。
> C. 线性表若采用链式存储表示时所有结点之间的存储单元地址可连续可不连续。
> D. 二维数组是每个元素都为线性表的线性表 .
> E. 每种数据结构都应具备三种基本运算：插入、删除和搜索。
> **CD**

**Reason:** A. 线性表逻辑上是线性的，存储上可以是顺序或链式存储；B. 各有优缺点；E. 数据结构需要的基本操作中，搜索不是必须的，比如栈、队列；多维数组没有插入和删除

> 5. 稀疏矩阵可以采用三元组顺序表方法压缩存储.
**True**

**note:** 三元组是（行坐标，列坐标，值），稀疏矩阵有两种压缩方式：三元组和十字链表；稀疏矩阵是指矩阵中0元素数量远多于非0元素，且0的分布没有规律

> 6. `char a[] = "abcd"` 和`char b[] = {'a','b','c','d'}`这两种表达方式等价。
**False**

**Reason：** sizeof(a)的值会比sizeof(b)大1。

> 7. 若定义：char s[20]="programming",\*ps=s ；
则不能表示字符‘o’的是( )。
> A. ps+2
> B. s[2]
> C. ps[2]
> D. \*(ps+2)
**A**

**Reason:** ps为指针，ps+2为一个地址；当ps为指针时，ps[2]等价于s[2]；\*(ps+2)，取到了ps[2]的值。

> 8. （多选）在java当中，下列关于数组的说法错误的有( )
> A. 数组是一种对象
> B. 数组属于一种原生类
> C. int number = [] = {31,23,33}
> D. 数组大小可以任意改变
**BCD**

**Reason：** a、数组是能被Object 一切能被Obj 接收的均为对象； b、数组不是原生类 原生类有8种， int、double、boolean、float、byte、short、long、char ； c、语法错误、 d、数组的大小一开始就已经确定了 int[]test=new test[2];


> 9. 设有一个 10 阶的下三角矩阵 A （包括对角线），按照行优先的顺序存储到连续的 55 个存储单元中，每个数组元素占 1 个字节的存储空间，则 A[5][4] 地址与 A[0][0] 的地址之差为（ ）。
> A. 10
> B. 19
> C. 28
> D. 55
**B**

**Reason:** 1+2+3+4+5+6-1 = 19。这一题错是因为我少数了一行orz

> 10. 数组插入或删除元素的时间复杂度O(n)，链表的时间复杂度O(1)
**False**

**Reason:** 链表只有删除尾部元素时复杂度才是O(1)，删除中间部分元素时，复杂度也是O(n)，需要先查找到对应的位置。


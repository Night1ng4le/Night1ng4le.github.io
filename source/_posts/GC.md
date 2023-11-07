---
title: GC读书笔记
categories: [Advanced]
tags: [Garbage Collection,note]
---

最近一个作业涉及这方面的内容，所以记一下这部分的内容。书的链接[<<垃圾回收的算法与实现>>](https://item.jd.com/12010270.html)

##### GC的定义
GC（Garbage Collection，垃圾回收）要做的两件事：
- 找到内存空间里的垃圾
- 回收垃圾，让程序员能再次利用这部分空间
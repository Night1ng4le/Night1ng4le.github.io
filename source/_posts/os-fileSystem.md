---
title: OS - 文件系统
categories: [CS Basis]
tags: [OS]
---
这个系列的文章都是学习清华《操作系统》（向勇、陈渝老师）的时候自己做的课程笔记。
视频来源：学堂在线
本章笔记主要是文章系统相关知识，这一章概念比较多一些，宜多看几遍尝试理解

<!-- more -->

### 文件系统的概念
#### 文件系统和文件
文件系统是操作系统中管理持久数据的子系统，提供数据存储和访问功能。
- 组织、检索、读写访问功能

文件是具有符号名，由字节序列构成的数据项的集合
- 文件系统的基本数据单位
- 文件名是文件的标识符号

#### 文件系统的功能
- 分配文件磁盘空间
	- 管理文件块（位置和顺序）
	- 管理空闲空间（位置）
	- 分配算法（策略）
- 管理文件集合
	- 定位：找到文件的位置
	- 命名：通过名字找到文件
	- 文件系统结构：文件组织方式
- 数据可靠和安全
	- 安全：多层次保护数据安全
	- 可靠：
		- 持久保存文件
		- 避免系统崩溃、媒体错误、攻击等

#### 文件属性
- 文件头：文件系统元数据中的文件信息
	- 文件属性
	- 文件存储位置和顺序

#### 打开文件
- 文件访问模式
	- 进程访问文件数据前必须先“打开”文件
- 内核跟踪进程打开的所有文件
	- OS为`每个进程`维护一个打开文件表
	- 文件描述符是打开文件的标识（文件描述符比文件标识更简单）

#### 文件描述符
操作系统在打开文件表中维护的打开文件的状态和信息
- 文件指针：
	- 指向最近一次读写位置
	- 每个进程分别维护自己的打开文件指针
- 文件打开计数
	- 当前打开文件的次数
	- 用于最后一个进程关闭文件的时候，将其从打开文件列表移除
- 文件的磁盘位置：缓存数据访问信息
- 访问权限：每个进程的文件访问模式


#### 文件的用户视图和系统视图
- 文件的用户视图
	- 持久的数据结构

- 系统访问接口
	- 字节序列的集合
	- 系统不关心存储在磁盘上的数据结构

- 系统视图
	- 数据块的集合
	- 数据块是逻辑存储单元，扇区是物理存储单元
	- 块大小和扇区大小的关系（通常是几个扇区构成一个数据块）

#### 用户视图到系统视图的转换
- 进程读文件
- 进程写文件
- `文系统中的基本操作单位是数据块`。对磁盘的访问中，读一个字节要整块读出来，写一个字节要整块重新写。

#### 访问模式
- 顺序访问：按字节依次读取（大多数文件）
- 随机访问：从中间读写
	- 不常用，例如虚拟存储中把内存页存储在对换文件中，即随机访问
- 索引访问：依据数据特征索引
	- 通常操作系统不完整提供索引访问
	- 数据库是建立在索引内容的磁盘访问上

#### 文件内部结构
- 无结构
	- 单词、字节序列
- 简单的记录结构
	- 分列（定长or不定长）
- 复杂结构

#### 文件共享和访问控制
- 多用户系统中文件共享是必要的
- 访问控制
	- 每个用户能够获得的文件访问权限
	- 模式：读、写、执行、删除、列表
- 文件访问控制表（ACL）

#### 分层文件系统
- 文件以目录的方式组织起来
- 目录是一类特殊的文件
	- 目录的内容是文件索引表<文件名，指向文件的指针>
- 目录和文件的树形结构
	- 早起的文件系统是扁平的（一层目录）
	- 每个文件都对应唯一一条从根目录到文件本身的路径
- 目录操作
	- 搜索、创建、删除、列目录
	- 重命名、遍历路径
- 操作系统只允许内核修改目录
	- 确保映射完整性
	- 应用程序通过系统调用访问目录

#### 目录实现
- 线性列表（含指向数据块的指针）
	- 编程简单
	- 执行耗时
- `哈希表` - 哈希结构的线性表
	- 减少目录搜索时间
	- 文件名哈希值相同时产生冲突
	- 目录表每一项固定大小

#### 文件别名
两个或多个文件名关联同一个文件
- 硬连接：多个文件指向一个文件
	- 最后一个指向该文件的指针删除的时候，文件才是真的删除
- 软连接：以“快捷方式”指向其他文件
	- 通过存储真实文件的逻辑名称来实现
	- 删除文件别名和删除文件是一样的
- 保证文件目录中的循环
	- 只允许到文件的链接，不允许在子目录的链接
	- 增加链接时，用循环检测算法确定是否合理（）



### 虚拟文件系统（VFS）
#### 概述
- 分层结构
- 目的：对所有不同文件系统的抽象
- 功能：
	- 相同的文件和文件系统接口
	- 管理相关数据结构
	- 查询例程（高效遍历）
	- 与特定文件系统模块交互

#### 文件系统基本数据结构
- 文件卷控制块（文件系统）- 挂载时进入内存
- 文件控制块（文件）- 文件被访问时进入内存
- 目录项 - 遍历文件路径时进入内存

#### 文件系统存储结构
持久的存储在外存中，需要时加载进内存

#### 文件的组织方式
- 顺序文件（批量存取）
	- 串结构：按存入时间的先后进行排序，每次检索从头开始
	- 顺序结构：按关键字进行排序，利用关键字特征结合查找算法进行查找
- 索引文件（增删查改单个记录）

- 索引顺序文件


### 文件缓存和打开文件


### 文件分配

### 空闲空间管理

### 冗余磁盘阵列RAID













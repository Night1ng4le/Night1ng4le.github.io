---
title: Stack
categories: [Leetcode]
tags: [Data structure] 
---




### 概述
复习栈的数据结构的一些笔记，比较零碎。

<!--more-->

![alt](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/06/03/screen-shot-2018-06-02-at-203523.png)

#### 栈的实现:
**Leetcode版**
利用向量实现，直接调用向量的接口。
```c++
#include <iostream>

class MyStack {
    private:
        vector<int> data;               // store elements
    public:
        /** Insert an element into the stack. */
        void push(int x) {
            data.push_back(x);
        }
        /** Checks whether the queue is empty or not. */
        bool isEmpty() {
            return data.empty();
        }
        /** Get the top item from the queue. */
        int top() {
            return data.back();
        }
        /** Delete an element from the queue. Return true if the operation is successful. */
        bool pop() {
            if (isEmpty()) {
                return false;
            }
            data.pop_back();
            return true;
        }
};
```

**原始版**
使用普通数组实现
```c++
//这个是我自己写的，也可能哪里不对？
class Stack{
private:
    int _size;
    int a[N];
public:
    Stack(){
        _size = 0;
    }
    char* pop(){
        return a[--_size];
    }
    void push(int e){
        a[_size++]=e;
    }
    bool empty(){
        return _size<=0;
    }
    char* find(int index){
        return a[index-1];
    }
};
```

#### 调用
c++内置栈库是可以直接调用的。使用栈的操作时，需要注意的是，调用pop函数时，一定要先判断栈是否为空。

### 栈应用
#### 分类
- 逆序输出（conversion）

- 递归嵌套（stack permutation+parenthesis）
	
- 延迟缓冲（evaluation）
	- 线性扫描算法模式中，在预读足够长之后，方能确定可处理的前缀
- 栈式计算（RPN）
	- 逆波兰表达式

#### 逆序输出
**特点**
- 输出次序与处理过程颠倒
- 递归深度和输出长度不易预知

**实例：进制转换**
- 短除法
- 借助辅助栈，每计算出一个就push进栈
- 全部计算完成后，连续的pop直至栈空

#### 递归嵌套
**特点**
- 具有自相似性的问题可递归描述，但分支位置和嵌套深度不固定

**实例：括号匹配**



### 经典题目

[最小栈](https://nighting4le.com/2020/04/21/Leetcode-155-minStack/)
[有效的括号](https://nighting4le.com/2020/04/21/Leetcode-20-isValid/)
[柱状图中最大矩形](https://nighting4le.com/2020/04/11/Leetcode-84.%E6%9F%B1%E7%8A%B6%E5%9B%BE%E4%B8%AD%E6%9C%80%E5%A4%A7%E7%9F%A9%E5%BD%A2/)
[最大矩形](https://nighting4le.com/2020/04/13/Leetcode-85-%E6%9C%80%E5%A4%A7%E7%9F%A9%E5%BD%A2/)
[每日温度](https://nighting4le.com/2020/05/02/Leetcode-739.dailyTemp/)
[逆波兰表达式](https://nighting4le.com/2020/05/03/Leetcode-150-evalRPN/)



**参考链接**
- 《数据结构》，邓俊辉 —— https://next.xuetangx.com/course/THU08091000384/1516243
- Leetcode探索【栈和队列】—— https://leetcode-cn.com/explore/learn/card/queue-stack/218/stack-last-in-first-out-data-structure/875/










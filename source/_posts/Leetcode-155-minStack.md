---
title: Leetcode 155. 最小栈
categories: [Leetcode]
tags: [Stack,Data Structure]
---

### Description
设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

- push(x) —— 将元素 x 推入栈中。
- pop() —— 删除栈顶的元素。
- top() —— 获取栈顶元素。
- getMin() —— 检索栈中的最小元素。

<!--more-->

**示例**
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```


### Solution
因为感觉这一题想要考察的关键点不是栈基本操作实现，所以就没有自己实现栈。这里的核心应该是如何实现getMin()，所以维护两个栈，其中一个是用于实时更新最小值的辅助栈。
我踩过的坑：
    1. 最小值需要实时更新，所以用栈比用变量简单一些
    2. data和_min的pop操作未必是同步的
    3. 和_min栈顶相等的元素也要push进去，判断条件应该是“≤”

```c++
class MinStack {
   
public:
    stack<int> data;
    stack<int>  _min;
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        data.push(x);
        if (_min.empty()||x<=_min.top()) {//注意这里应该是≤，相等的元素也要入栈，否则会不够用。
            _min.push(x);
        }
    }
    
    void pop() {
        if (data.top()==_min.top()) {
            _min.pop();
        }
        data.pop();
    }
    
    int top() {
        return data.top();
    }
    
    int getMin() {
        int min =  _min.top();
        return min;
    }
};
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */

```
这里自己踩到的坑就是push判断的时候的小于等于这里，边界情况需要特别注意。
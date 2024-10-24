---
title: Leetcode面试0305 - stackSort
categories: [Leetcode]
tags: [Algorithm Training,Stack,sort]
---


### Problem Link
https://leetcode-cn.com/problems/sort-of-stacks-lcci/

### Description
栈排序。 编写程序，对栈进行排序使最小元素位于栈顶。最多只能使用一个其他的临时栈存放数据，但不得将元素复制到别的数据结构（如数组）中。该栈支持如下操作：push、pop、peek 和 isEmpty。当栈为空时，peek 返回 -1。

<!--more-->

**示例1:**
```
 输入：
["SortedStack", "push", "push", "peek", "pop", "peek"]
[[], [1], [2], [], [], []]
 输出：
[null,null,null,1,null,2]
```
**示例2:**
```
 输入： 
["SortedStack", "pop", "pop", "push", "pop", "isEmpty"]
[[], [], [], [1], [], []]
 输出：
[null,null,null,null,null,true]
```
**说明:**

*栈中的元素数目在[0, 5000]范围内。*



### Solution

 StackSort（栈排序）的本质其实是用栈实现的插入排序。对于插入排序而言，任一时刻，当前元素的左侧必然都是有序的。所以使用两个栈，将已经有序的部分存放入栈S（sort），未排序的部分存放在栈R（Random）。
 同时StackSort要求只能额外使用O(1)的空间，因此需要善用栈R来帮忙。将S栈pop出的元素push到R栈中，即可实现空间需求。

```
 -------------  ---    ----------------
|  S (sorted)  | e |       R(random)   |   
 -------------  ---    ----------------
                 ^
                 |
               当前元素
#大致思路
if(S.top()≥t)
	S.push(t);
	t=R.pop();
else
	R.push(S.pop());

```
这里要注意边界条件，比如R栈只有一个元素的情况，比如S栈何时为空等。
```c++
class SortedStack {
private:
    stack<int> S;
    stack<int> R;
public:
    SortedStack() {
        
    }
    
    void push(int val) {//根据题意，push函数用来实现排序功能
        while(!S.empty()&&val>S.top()){//每次进行top操作都要保证栈非空
            R.push(S.top());
            S.pop();
        }
        S.push(val);
        while(!R.empty()){//把弹出去的有序元素还放回来
            S.push(R.top());
            R.pop();
        }
    }
    
    void pop() {
        if(!S.empty()){
            S.pop();
        }
    }
    
    int peek() {
        if(isEmpty()){
            return -1;
        }
        else
           return S.top();
    }
    
    bool isEmpty() {
        return S.empty();
    }
};

/**
 * Your SortedStack object will be instantiated and called as such:
 * SortedStack* obj = new SortedStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->isEmpty();
 */
```

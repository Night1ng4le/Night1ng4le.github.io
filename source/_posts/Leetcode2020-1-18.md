---
title: Leetcode - Moving Average from Data Stream
categories: [Leetcode]
tags: [Queue]
---


### Problem Link

https://leetcode-cn.com/explore/learn/card/queue-stack/216/queue-first-in-first-out-data-structure/868/

<!--more-->

### Description

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

**Example:**
```c++
MovingAverage m = new MovingAverage(3);
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3
```

### Solution

```c++
class MovingAverage {
private:
    queue<int> data;
    int size;  //窗口大小
    double sum;
    
public:
    /** Initialize your data structure here. */
    MovingAverage(int size) {
        this->size = size;  //窗口大小
        sum = 0;  
    }
    
    double next(int val) {
        double avg = 0; //平均值
        if(data.size()>=size){    //如果添加新元素超出窗口
            sum -= data.front();  //减去首元素
            data.pop();  //首元素出队
        }
        data.push(val);  //新元素入队
        sum += data.back();  
        avg = sum/data.size();
        return avg;
    }
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage* obj = new MovingAverage(size);
 * double param_1 = obj->next(val);
 */


```

### Sth else
复习队列的第一道题，写的时候有一点卡，大概是时隔半年终于重新开始跟代码死磕了。一开始没太明白这题想干嘛，就是隐约有个思路，然后就推不动了，差点自己实现一波队列...我知道这是个简单题，然而...现实就是我卡了一天。希望后续会好一点（我应该会写一段时间的注释ovo）

test
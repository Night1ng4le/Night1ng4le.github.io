---
title: 84. 柱状图中最大矩形
categories: [Leetcode]
tags: [Stack,Algorithm Training]
---



### Problem Link
https://leetcode-cn.com/problems/largest-rectangle-in-histogram/

### Description
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。
<!--more-->

![alt](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 `[2,1,5,6,2,3]`。

![alt](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)
图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

> **示例:**
>
> 输入: [2,1,5,6,2,3]
> 输出: 10


### Solution

问题分析：
- 若矩形的底是从位置a到位置b
- 底 = b-a+1，高 = min{hi|a≤i≤b}
- S = (b-a+1)\*min{hi|a≤i≤b} 

#### Version 0 - 蛮力算法

基于问题分析，最容易想到的是蛮力算法。通过二重循环枚举求出底边（a≤b），再利用第三重循环枚举最小的底边高度。此时的时间复杂度是O(n<sup>3</sup>)。

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int ans = 0;
        int S;
        for(int a=0;a<heights.size();a++){
            for(int b=a;b<heights.size();b++){
                int minH = 2147483647;//这个数是我根据测试数据设的，正无穷更好一点
                for (int c=a; c<=b; c++) {//求min{hi|a≤i≤b}
                    minH = min(minH,heights[c]);
                }
                ans = max(ans,(b-a+1)*minH);
            }
        }
        return ans;
    }
};
```

#### Version 1 - 蛮力算法优化

显然无法优化枚举底边的过程，只能优化求高的过程。这里注意到a到b的最小高度H<sub>1</sub>和a到b+1的最小高度H<sub>2</sub>之间的关系为
H<sub>2</sub> = min{H<sub>1</sub>,h<sub>b+1</sub>}，此时轻易的可以去掉一层循环。此时的时间复杂度是O(n<sup>2</sup>)。
```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int ans = 0;
        for(int a=0;a<heights.size();a++){
            int minH = INT_MAX;
            for(int b=a;b<heights.size();b++){//把最里层循环去掉
                minH = min(minH,heights[b]);
                ans = max(ans,(b-a+1)*minH);
            }
        }
        return ans;
    }
};
```

#### Version 2 - 单调栈

优化后的蛮力算法，时间复杂度依旧不令人满意，所以使用第二种方法。这里利用单调栈，实现时间复杂度为O(n)的算法。

```

          ----
         |    |         ---
  ---    |    |        |   |
 |   |   |    |        |   |
 |   |   |    |        |   |
 |   |   |    |        |   |
 |   |   |    |        |   |
 |   |   |    |        |   |
--------------------------------------
 i(k)      k            j(k)

  --------------------------------
 |                    ----   ---                    
 |                   |i(k)| | k |
 |                    ----   ---
  --------------------------------

  小---------------------------->大
```
k为当前时刻的局部最小值，对于每一个k来说它的两侧，必有一个卡点（可能是哨兵）。遍历直方图的高，栈中存储的是当前时刻元素左边经过筛选的元素。i(k)是k左侧第一个小于k的元素，同理i(k)的前一个元素应该是i
(k)左侧第一个小于它的元素。显然，栈中元素是单调的，当前遍历至第一个小于栈顶元素的元素，则应该是栈顶元素对应的右侧卡点，此时即可计算出maxRect的候选者之一。


```c++
class Solution {
public:
     int largestRectangleArea(vector<int>& heights) {
        int ans = 0;
        stack<int> myStack;
        vector<int> myHeight(heights.size()+2);
        for(int i=1;i<heights.size()+1;i++){
            myHeight[i] = heights[i-1];
        }
        myStack.push(0);
        for (int i=1; i<=heights.size()+1; i++) {
            while (myHeight[i]<myHeight[myStack.top()]) {
                int nowheight = myHeight[myStack.top()];
                myStack.pop();
                ans = max(nowheight*(i-myStack.top()-1), ans);
            }
            myStack.push(i);
        }
        
        return ans;
    }

};
```


### Some tips
> - n ≤ i * 1000 -----> O(n<sup>2</sup>)，O(n<sup>2</sup>logn)的算法可用
> - n ≤ i * 10000 ----> O(n)，O(nlogn)，O(nlog<sup>2</sup>n)的算法可用





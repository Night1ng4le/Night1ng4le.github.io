---
title: Leetcode - 69. x的平方根
categories: [Leetcode]
tags: [Binary Search]
---


### Description
实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

<!--more-->

**示例 1:**
输入: 4
输出: 2

**示例 2:**
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。

### Solution
#### 二分查找
这是一个比较粗略的解法。对于x<2的情况，直接返回x；对x≥2，x的平方根必然在(0,x/2)之间。所以这个问题就变成了折半查找特定值的问题。
![alt](https://pic.leetcode-cn.com/Figures/69/binary.png)

**算法**

- 如果 `x < 2`，返回 `x`
- 令左边界为 `2`，右边界为 `x/2`
- 当 `left <= right` 时：
	- 令 `num = (left + right) / 2`，比较 `num * num` 与 `x`：
		- 如果 `num * num > x`，更新右边界为`right = pivot -1`
		- 如果 `num * num < x`，更新左边界为 `left = pivot + 1`
		- 如果 `num * num == x`，即整数平方根为 `num`，返回 `num`
- 返回 `right`

**代码**
```c++
class Solution {
public:
    int mySqrt(int x) {
        if (x<2)  return x;
        long ans;
        int left = 2;
        int right = x/2;
        while (left<=right) {
            int mid = (left + right)/2;
            ans = (long)mid*mid;
            if (ans>x) right = mid-1;
            else if(ans<x) left = mid+1;
            else return mid;
        }
        return right;
    }
};
```

---
title: Leetcode - 374. 猜数字大小
categories: [Leetcode]
tags: [Binary Search]
---

### Description
我们正在玩一个猜数字游戏。 游戏规则如下：
我从 1 到 n 选择一个数字。 你需要猜我选择了哪个数字。
每次你猜错了，我会告诉你这个数字是大了还是小了。
你调用一个预先定义好的接口 guess(int num)，它会返回 3 个可能的结果（-1，1 或 0）：

<!--more-->

-1 : 我的数字比较小
1 : 我的数字比较大
0 : 恭喜！你猜对了！

`注：guess接口返回的1与-1的意思与题意相反，不要怀疑自己的脑子`

**示例 :**
输入: n = 10, pick = 6
输出: 6


### Solution
#### 蛮力算法
```c++
class Solution {
public:
    int guessNumber(int n) {
        for(int i=1;i<n;i++){
            if(guess(i)==0)
                return i;
        }
        return n;
    }
};
```
时间复杂度O(n)
这种解法没有充分用到guess的返回值，并且时间复杂度不满足要求。


#### 二分查找
```c++
int guessNumber(int n) {
        int left = 1;
        int right = n;
        int mid;
        while(left<=right){
            mid = (left+right)/2;
            if(guess(mid)==0) return mid;
            else if(guess(mid)==-1) right = mid-1;
            else left = mid+1;
        }
        return -1;
    }
```
时间复杂度O(logn)




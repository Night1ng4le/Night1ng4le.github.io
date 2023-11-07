---
title: Leetcode 85. 最大矩形
categories: [Leetcode]
tags: [Stack,Algorithm Training]
---

### Problem Link
https://leetcode-cn.com/problems/maximal-rectangle/

### Description
给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

<!--more-->

**示例:**

```
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```

### Solution

这一题属于84改编的一道进阶题，并没有很难。在知道如何求直方图中的最大矩形之后，使用一个for循环，对每一行求一次直方图的最大面积

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

    int maximalRectangle(vector<vector<char>>& matrix) {
        if (matrix.size()==0) {
            return 0;
        }
        int ans = 0;
        vector<int> height(matrix[0].size());
        for (int i = 0; i<matrix.size();i++) {
        
            for (int j=0; j<matrix[0].size(); j++) {
                if (matrix[i][j] == '1') {
                    height[j]++;
                }else{
                    height[j] = 0;
                }
            }
            ans = max(ans, largestRectangleArea(height));
        }
        return ans;
    }
};


/*
这一题代码错误点：
	1. 一开始没打算直接调用函数，所以maximalRectangle的height数组大小后来忘记改
	2. if语句判断当前元素是否为1的时候恒等写成了赋值

*/
```

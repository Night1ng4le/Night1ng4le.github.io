---
title: Leetcode 5401. 是否所有 1 都至少相隔 k 个元素
categories: [Leetcode]
tags: [Stack,Week Contest]
---

### Description
给你一个由若干 0 和 1 组成的数组 nums 以及整数 k。如果所有 1 都至少相隔 k 个元素，则返回 True ；否则，返回 False 。
<!--more-->

**示例 1：**
![alt](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/05/03/sample_1_1791.png)
*输入：*nums = [1,0,0,0,1,0,0,1], k = 2
*输出：*true
*解释：*每个 1 都至少相隔 2 个元素。

**示例 2：**
![alt](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/05/03/sample_2_1791.png)
*输入：*nums = [1,0,0,1,0,1], k = 2
*输出：*false
*解释：*第二个 1 和第三个 1 之间只隔了 1 个元素。

**示例 3：**

*输入：*nums = [1,1,1,1,1], k = 0
*输出：*true

**示例 4：**
*输入：*nums = [0,1,0,1], k = 1
*输出：*true

**提示：**
- 1 <= nums.length <= 10^5
- 0 <= k <= nums.length
- nums[i] 的值为 0 或 1


### Solution

这一题我用的还是辅助栈的解法，最近复习这个套路所以用的比较熟一点。这题比每日温度还要再简单一点。栈在处理这一类问题的时候真的很好用。
我自己感觉辅助栈这个系列的难度是排序是：
`这一题 < 每日温度 < 柱状图中最大矩形 < 不规则图形中的最大矩形`
```c++
class Solution {
public:
    bool kLengthApart(vector<int>& nums, int k) {
        stack<int> S;
        bool ans = true;
        for (int i=0; i<nums.size(); i++) {
            if (nums[i]==0){
                continue;
            }
            if (!S.empty()) {
                if (i-S.top()-1<k) {
                    ans = false;
                    break;
                }
            }
            S.push(i);
        }
        return ans;
    }
};
```
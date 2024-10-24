---
title: 每日一题笔记 - Week 1
categories: [Leetcode]
tags: [每日一题,Coding]
---

上周每日一题的笔记小结（没有涉及困难题）

<!--more-->

### 1774. 最接近目标价格的甜点成本（Medium）

**题目描述：**https://leetcode.cn/problems/closest-dessert-cost/

算是动态规划？
是一道写完也没有完全懂的题，我是按0-1背包的思路理解的代码，后续可能需要再多看几次，努力掌握精髓。

```c++
class Solution {
public:
    void dfs(int curCost, int& minAns, int& target, const vector<int>& toppingCosts, int p) {
        if ((curCost - target) > abs(minAns - target)) { // curCost > target &&  calculate difference
            return;
        }
        else if (abs(curCost - target) <= abs(minAns - target)) {
            if(abs(curCost - target) < abs(minAns - target)) {
                minAns = curCost;
            }
            else{
                minAns = min(curCost, minAns);
            }
        }
        if(p == toppingCosts.size()) return;
        dfs(curCost + toppingCosts[p], minAns, target, toppingCosts, p+1);
        dfs(curCost + toppingCosts[p] * 2, minAns, target, toppingCosts, p+1);
        dfs(curCost, minAns, target, toppingCosts, p+1);
    }
    int closestCost(vector<int>& baseCosts, vector<int>& toppingCosts, int target) {
        // 回溯
        int minAns = *min_element(baseCosts.begin(), baseCosts.end()); // 最小是只有一个base的时候
        for (auto& a : baseCosts) {
            dfs(a, minAns, target, toppingCosts, 0);
        }
        return minAns;
    }
};
```

### 1805. 字符串中不同整数的数目（Easy）

**题目描述：**https://leetcode.cn/problems/number-of-different-integers-in-a-string/

#### Solution 1 一种只适合python，但c++和Java就会溢出的方法

如果一个很长的字符串都是数字，就会出现溢出（累了

```c++
class Solution {
public:
    int numDifferentIntegers(string word) {
        int n = word.length();
        unordered_set<long> nums;
        long sum = 0; // calculate number

        // check first number
        if('1' <= word[0] && word[0] <= '9') {
            sum = word[0];
        }
        for (int i = 1; i < n; i++) {
            if (word[i] < '0' || word[i] > '9'){
                if ('0' <= word[i-1] && word[i-1] <= '9') {
                    nums.emplace(sum); // record different number
                    sum = 0; // reset sum
                }
                // printf("%c", word[i-1]);
                continue;
            } 
            else {
                sum = sum * 10 + word[i]-48;
            }
        }
        if (sum) {
            nums.emplace(sum);
        }
        return nums.size();
    }
};
```

#### Solution 2 不得不学习的c++双指针法

一开始想到过双指针（人还是要相信一闪而过的念头），但我自己不知道怎么精妙的使用双指针，直到看见大佬的解决方案
- 从第一个是数字的字符开始循环，右指针停在后续第一个不是数字的字符的位置。
- 更新左指针位置的时候，跳过已经录入的数字部分，避免无效遍历

```c++
class Solution {
public:
    int numDifferentIntegers(string word) {
        // initialize
        int n = word.length();
        unordered_set<string> map;
        for(int i = 0; i < n; i++) {
            if(isdigit(word[i])){
                int j = i;
                while(j < n && isdigit(word[j])) j++;
                while(word[i] == '0') i++;  // remove '0'
                map.emplace(word.substr(i, j-i)); // trick
                i = j;
            }
        }
        return map.size();
    }
};
```

`Note:`
1. substr(begin_pos, len) - 这个函数len = 0 时，substr返回空字符串，emplace()会把空字符串当作0处理，所以只有一个0的情况也不会发生错误。
2. emplace()的效率高于insert()

### 144. 二叉树前序遍历（乱入的Easy）

只是复习一下前序遍历的写法

#### Solution 1 递归
```c++
// 递归版
class Solution {
public:
    void travel(TreeNode* root, vector<int>& arr) {
        if(root == NULL) {
            return;
        }
        arr.push_back(root->val);
        travel(root->left, arr);
        travel(root->right, arr);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> arr;
        travel(root, arr);
        return arr;
    }
};
```

#### Solution 2 迭代

```c++

```

### 1775. 通过最少操作次数使数组的和相等（Medium）

**题目描述：** https://leetcode.cn/problems/equal-sum-arrays-with-minimum-number-of-operations/

#### Solution

> - 判断什么情况下数组的和有可能相等:将和较小的数组每个数字变成6，将和较大的数组每个数字变成1。如果此时较小的数组之和仍小于较大的数组，则`return -1`
> - 假设nums1的和大于nums2，否则交换两个数组
> - nums1每个元素值可以变化`nums[i]-1`， nums2每个元素的值可以变化`6-nums2[i]`
> - 使用一个大小为6的数组，记录差值为0，1，2，3，4，5的个数；反向遍历即可找到最少的步数。

```c++
class Solution {
public:
    int minOperations(vector<int>& nums1, vector<int>& nums2) {
        // check impossible
        if (6 * nums1.size() < nums2.size() || 6 * nums2.size() < nums1.size()) return -1; // 优化，这种情况肯定无解
        // initialize
        int sum = accumulate(nums1.begin(), nums1.end(), 0) - accumulate(nums2.begin(), nums2.end(), 0); // 假设nums1的和大于nums2
        if (sum < 0) { // 强制nums1和大，nums2的和小
            sum = -sum;
            swap(nums1, nums2);
        }
        // count
        int count[6]{}; // 使用一个长度为6的数组作为计数器，统计差值出现的频次，下标是差值，值是频次
        for(int x : nums2) count[6-x]++; // nums2所有元素替换为6
        for(int x : nums1) count[x-1]++; // nums1所有元素替换为1
        for(int i = 5, res = 0; ; i--) {
            if(i * count[i] >= sum) {
                return res + (sum + i -1) / i; // (sum + i -1) / i，这里+i是因为结果向上取整，-1时考虑到如果sum是i的倍数，向上取整结果会多1，-1就可以避免这种情况的发生。
            }
            res += count[i];
            sum -= i * count[i];
        }
    }
};
```

### 1812. 判断国际象棋棋盘格子的颜色（Easy）

**题目描述：**https://leetcode.cn/problems/determine-color-of-a-chessboard-square/

#### Solution
```c++
// 傻瓜式写法
class Solution {
public:
    bool squareIsWhite(string coordinates) {
        if((coordinates[0] - 'a') % 2 == 0){
            if(coordinates[1] % 2 == 0) return true;
            else return false;
        } else{
            if(coordinates[1] % 2 == 0) return false;
            else return true;
        }
    }
};
```

```c++
// 题解的写法
class Solution {
public:
    bool squareIsWhite(string coordinates) {
	return (coordinates[0] + coordinates[1]) % 2;
    }
};
```


### 1780. 判断一个数字是否可以表示成三的幂的和（Medium）

**题目描述：**https://leetcode.cn/problems/check-if-number-is-a-sum-of-powers-of-three/

两种思路本质上都以进制转换为基础写的，区别在于我自己写进制转换的脑回路和大多数人不一样orz

#### Solution 1 模拟进制转换（我的思路）

我是按照我手写10进制转2进制的思路来的。
- 先找到一个不大于n的最大的3的次幂，记做subNum
- 从最大的subNum开始，进行以3为基数的二进制转换（因为每个subNum只能使用一次）

```c++
class Solution {
public:
    int findI(int n) {
        int i = 1;
        while (n >= i) {
            i = i * 3;
        }
        return i / 3;
    }
    bool checkPowersOfThree(int n) {
        int subNum = 1;
        if (n == 0) {
            return false;
        }
        subNum = findI(n);
        while (n >= 0) {
            if(n == 0) return true;
            if (subNum > 0) {
                if (n >= subNum) {
                    n = n - subNum;
                }
                subNum = subNum / 3;
            } else {
                return false;
            }
        }
        return false;
    }
};
```

#### Solution 2 更普遍的解法（题解里大家的写法）

直接进行10进制转3进制，3进制的结果中一旦出现2，即`return false`。

```c++
class Solution {
public:
    bool checkPowersOfThree(int n) {
        while(n > 0) {
            if (n % 3 == 2){   
                return false;
            }
            n = n / 3;
        }
        return true;
    }
};
```

### 1796. 字符串中第二大的数字（Easy）

**题目描述：** https://leetcode.cn/problems/second-largest-digit-in-a-string/

#### Solution

用两个指针记录最大值和次大值，每次比较更新即可

```c++
class Solution {
public:
    int secondHighest(string s) {
        int i = 0;
        int f_max = -1;
        int s_max = -1;
        // unordered_set<int> num;
        while (s[i] != '\0') {
            if ('0' <= s[i] && s[i] <= '9'){
                int temp = s[i] - '0';
                if (f_max < temp) {
                    s_max = f_max;
                    f_max = temp;
                } else if (s_max < temp && temp < f_max) {
                    s_max = temp;
                }
            }
            i++;
        }
        if (s_max >= 0) {
            return s_max;
        }
        return -1;
    }
};

```

希望这周一切顺利🎐
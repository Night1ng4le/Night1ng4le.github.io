---
title: Leetcode - Minimum Number of Steps to Make Two Strings Anagram
categories: [Leetcode]
tags: [Week Contest,Medium]
---

### Problem Link

https://leetcode-cn.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/

### Description

Given two equal-size strings s and t. In one step you can choose any character of t and replace it with another character.

Return the minimum number of steps to make t an anagram of s.

<!--more-->

An Anagram of a string is a string that contains the same characters with a different (or the same) ordering.

**Example 1:**
```
Input: s = "bab", t = "aba"
Output: 1
Explanation: Replace the first 'a' in t with b, t = "bba" which is anagram of s.
```

**Example 2:**
```
Input: s = "leetcode", t = "practice"
Output: 5
Explanation: Replace 'p', 'r', 'a', 'i' and 'c' from t with proper characters to make t anagram of s.
```

**Example 3:**
```
Input: s = "anagram", t = "mangaar"
Output: 0
Explanation: "anagram" and "mangaar" are anagrams. 
```

**Example 4:**
```
Input: s = "xxyyzz", t = "xxyyzz"
Output: 0
```

**Example 5:**
```
Input: s = "friend", t = "family"
Output: 4
```

**Constraints:**
>    1 <= s.length <= 50000
>    s.length == t.length
>    s and t contain lower-case English letters only.



### Solution
肺炎阻止了我出门的脚步，于是，我人生中第一次周赛就这样开始了🎐.这是175周周赛，四道题，一道简单，两道中等，一道难。1347是其中的一道中等题（也叫5333）。
第一眼看见以为是字符串匹配，细看发现不是。又很久不写代码了，隐约感觉有思路，但是抓不住它。我决定从最朴素最简单的思路开始写。

#### Version1.0 - 暴力解题
这个真的是最朴素的写法，真的很暴力，穷举思想，所以自然时间复杂度非常高，达到O(n^2)。不出意料，我失败了，n较大的测试用例会运行超时。
p.s: 这个写到一半的时候我才意识到，这个问题的重点是如何计数，并不是真的让你去替换不同的字符
```c++
//version 1.0  - O(n^2) 暴力解题
struct Node{
    string content;
    bool flag;
};
class Solution {
private:
    string s1[50000];
    Node t1[50000];
public:
    int minSteps(string s, string t) {
        int result = 0;
        for (int i=0; i<s.size(); i++) {
            s1[i] = s.substr(i,1);
        }
        for (int j=0; j<t.size(); j++) {
            t1[j].content = t.substr(j,1);
            t1[j].flag = false;
        }
        
        for (int i=0; i<s.size(); i++) {
            for (int j=0; j<t.size(); j++) {
                if (s1[i] == t1[j].content && t1[j].flag != true) {
                    t1[j].flag = true;
                    break;
                }
            }
        }
        for (int i=0; i<t.size(); i++) {
            if (t1[i].flag == false) {
                result += 1;
            }
        }
        return result;
    }
};

```

#### Version2.0 - 统计差别数
穷举的思路显然是不明智的，所以继续观察题目，尝试简化问题。写Version1.0的时候，我所遇到的问题是：1. 不知道遍历字符串中字符的合适的方法；2. 没有找到合适的计数策略。这两个问题后续都会被解决。
观察到问题的本质是计数，而计数的对象应该是s和t的差别数，更具体来说就是s中有而t中没有的部分。所以2.0的思路大致是这样的：遍历s，用计数数组统计s中出现过的26个字母及出现次数，每出现一次，就在相应位置+1；遍历t，如果对应位置数字大于0，说明s和t都出现一次这个字符，做-1操作。如果对应位置小于等于0，说明这是s中没有出现而t中出现的字符，计数一次。计数器count的结果，即我们需要的差别数。
特殊🌰：如果两个字符串中的字符完全相同，则表示遍历s时所有加的值，都在遍历t时被减去，即count应该为0。

这个方法的时间复杂度是O(n)。
```c++
//Version2.0 - 统计差别数
class Solution {
public:
    int minSteps(string s, string t) {
        int count = 0;
        int flag[26]={0};//计数数组
        for (char i:s) {//这里的循环是遍历字符串，访问每个字符
            flag[i-'a']++;
        }
        for (char i:t) {
            if (flag[i-'a'] > 0) {
                flag[i-'a']--;
            }else{
                count++;
            }
        }
        return count;
    }
};
```

#### Version3.0 - 统计差别数（双指针）
最后这种解法是看题解的时候参考了一个小姐姐的解法～很有趣的思路，所以就自己写了一下mark下来
我觉得她讲的特别清楚，附上主页链接🔗：https://leetcode-cn.com/u/yisin/
附上她的题解链接🔗：https://leetcode-cn.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/solution/shuang-zhi-zhen-fa-bu-xu-yao-shi-yong-e-wai-kong-j/

```c++
class Solution {
public:
    int minSteps(string s, string t) {
        int count = 0;
        int len = s.size();
        int i = 0, j = 0;
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        while (i<len&&j<len) {
            if (s[i] == t[j]) {//匹配成功
                i++;
                j++;
                count++;
            }else if (s[i]>t[j]){
                j++;
            }else{//s字符串中的字符没有匹配项，指针后移
                i++;
            }
        }
        return len-count;
    }
};
```

### 写在最后
- 清楚的认识到自己依旧是个小菜鸡，不过总是会一点点进步的嘛～镜子会加油的～❤
- 小小的立个flag：接下来的一个月，每天坚持磕一道题
- 一个月之后来反馈自己有没有进步

*See you next time～❤*

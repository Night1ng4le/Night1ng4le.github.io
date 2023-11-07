---
title: Leetcode 20. 有效的括号
categories: [Leetcode]
tags: [Stack,Data Structure]
---
### Description
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

<!--more-->

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

**示例 1:**
输入: "()"
输出: true

**示例 2:**
输入: "()[]{}"
输出: true

**示例 3:**
输入: "(]"
输出: false

**示例 4:**
输入: "([)]"
输出: false

**示例 5:**
输入: "{[]}"
输出: true

### Solution

这个是我一开始写的错误版本，试图维护两个栈，左右括号各一个，如果栈顶匹配，则弹出，直至不匹配直接返回false或栈空返回true。可能因为方法非常暴力，所以还没有运行到错误样例就超出时间限制了，是后来自己想的时候发现这样做不对。

*举个🌰*
"([)]"
这个字符串显然是不匹配的，若运行如下代码，则两个栈状态如下：
```
|   |    |   |
| [ |    | ] |
| ( |    | ) |
 ---      ---
 left    right
```
那么这时候输出的结果就会是true，显然错误。

这样写只考虑了左右括号的个数和单边的位置，并没有综合考虑两边括号匹配的顺序。（我在说什么...

```c++
//version - wrong
class Solution {
public:
    stack<char> left;
    stack<char> right;
    bool isValid(string s) {
        bool ans = false;
        for (int i=0; i<s.size(); i++) {
            if (s[i]=='('||s[i]=='['||s[i]=='{') {
                char a = s[i];
                left.push(a);
            }
            if (s[i]==')'||s[i]==']'||s[i]=='}') {
                char b = s[i];
                right.push(b);
            }
        }
        while (!left.empty()&&!right.empty()) {
            if (left.top()=='('&&right.top()==')') {
                ans = true;
            }else if (left.top()=='['&&right.top()==']'){
                ans = true;
            }else if(left.top()=='['&&right.top()==']'){
                ans = true;
            }
        }
        return ans;
    }
};

```

👇下面更新正确的写法：
这个题具体实现的方法有很多，思路本质是一样的。利用一个辅助栈，遇到左括号，入栈；遇到右括号，如果和栈顶左括号匹配，则出栈，不匹配，直接返回false。

这里实现的方法比较简单，每遇到一个左括号，push一个对应的有括号，若遇到有括号，则判断其是否与栈顶元素相同即可。

```c++
//version 2.0
class Solution {
public:
    bool isValid(string s) {
        if (s.empty()) return true;//若字符串为空
        stack<char> ch;
        for (int i=0; i< s.size(); i++) {
            if (s[i] == ')' || s[i] == ']' || s[i] == '}') {
                if (!ch.empty()&&s[i]==ch.top()) {
                    ch.pop();
                }else return false;
            }
            else
                switch (s[i]) {
                    case '(':
                        ch.push(')');
                        break;
                    case '[':
                        ch.push(']');
                        break;
                    case '{':
                        ch.push('}');
                        break;
                }
        }
        return ch.empty();//栈中是否还有未匹配的左括号。
    }

};

```


### Problem Link
https://leetcode-cn.com/problems/valid-parentheses/
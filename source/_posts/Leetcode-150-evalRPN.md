---
title: Leetcode - 150. 逆波兰表达式求值
categories: [Leetcode]
tags: [Stack]
---

### Background
逆波兰表达式（RPN）是一种后缀表示法，操作符在操作数的后面。不需要括号来标识操作符的优先级。

<!--more-->

### Description
根据逆波兰表示法，求表达式的值。

有效的运算符包括 +, -, \*, / 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

**说明：**

整数除法只保留整数部分。
给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

**示例 1：**
输入: ["2", "1", "+", "3", "\*"]
输出: 9
解释: ((2 + 1) * 3) = 9

**示例 2：**
输入: ["4", "13", "5", "/", "+"]
输出: 6
解释: (4 + (13 / 5)) = 6

**示例 3：**
输入: ["10", "6", "9", "3", "+", "-11", "\*", "/", "\*", "17", "+", "5", "+"]
输出: 22
解释: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22


### Solution
RPN的求值并不是很难，只要理解RPN的形成逻辑就可以。
基本思路是利用辅助栈，如果s是操作符，则弹出栈中需要的运算元素个数进行运算，并将结果压回栈中，如果s是数字，则直接入栈。处理完所有字符，栈顶结果即位RPN的值。

#### 伪代码(from wiki)
```
while 有输入
	读入下一个符号X
	IF X是一个操作数
		入栈
	ELSE IF X是一个操作符
		有一个先验的表格给出该操作符需要n个参数
		IF堆栈中少于n个操作数
			（错误） 用户没有输入足够的操作数
		Else，n个操作数出栈
		计算操作符。
		将计算所得的值入栈
	IF栈内只有一个值
		这个值就是整个计算式的结果
	ELSE多于一个值
		（错误） 用户输入了多余的操作数
```

#### 实现 
```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        if (tokens.size()==0) {
            return 0;
        }
        stack<int> S;
        int temp1,temp2;
        int ans = 0;
        for (string s:tokens) {
            if (s=="+"||s=="-"||s=="*"||s=="/") {
                temp1 = S.top();
                S.pop();
                temp2 = S.top();
                S.pop();
                if (s=="+") {
                    ans = temp1+temp2;
                }else if (s=="-"){
                    ans = temp2-temp1;
                }else if (s=="*"){
                    ans = temp2*temp1;
                }else if (s=="/"){
                    ans = temp2/temp1;
                }
                S.push(ans);
            }
            else{
                S.push(stoi(s));
            }
        }
        return S.top();
    }
};

```

### Problem Link
https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/
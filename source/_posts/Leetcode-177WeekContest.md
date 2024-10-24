---
title: Leetcode - 177周赛
categories: [Leetcode]
tags: [Week Contest]
---


### 5169. 日期之间隔几天(Easy)

#### Problem Link
https://leetcode-cn.com/problems/number-of-days-between-two-dates/

#### Description
请你编写一个程序来计算两个日期之间隔了多少天。

日期以字符串形式给出，格式为 YYYY-MM-DD，如示例所示。

<!--more-->
 
**示例 1：**
```
输入：date1 = "2019-06-29", date2 = "2019-06-30"
输出：1
```

**示例 2：**
```
输入：date1 = "2020-01-15", date2 = "2019-12-31"
输出：15
```

**提示：**

`给定的日期是 1971 年到 2100 年之间的有效日期。`

####Solution
这个题的思考过程大概是这样的：
1.0版本是想着按照字面意思直接计算两个日期之间的差值。于是就有很多问题需要解决，诸如两个年份的大小关系、两个日期之差是否满一年等（别问，问就是这都是我踩过的坑）。就是这个见鬼的思路导致我没时间看后面的题。
这个思路本身没问题，理论上也是对的，但是不容易实现，实现的难点就在于没有一个基准值，所以不能用一个标准，通用的解决问题。所以出现了2.0。
2.0版本的思路更新为找一个基准值，分别计算两个日期相对于基准日期的差值，把两次得到的结果求差取绝对值即可。根据提示所给的条件，日期有效值在1971-01-01～2100-12-31，所以选择1970-01-01作为基准值，即可统一计算标准。
```c++
class Solution {
private:
   int is4Times(int n){//判断闰年
            if(n%400==0)return 1;
            if(n%4==0 && n%100!=0)return 1;
            return 0;
        }

    int monthDay(int a,int b){//每月几天
        int day = 0;
        if (b==0) {
            day = 0;
        }else if (b==2) {
            if(is4Times(a)){
                day = 29;
            }else{
                day = 28;
            }
        }else if (b==4||b==6||b==9||b==11){
            day = 30;
        }else{
            day = 31;
        }
        return day;
    }
    int countDays(string date){//计算给定日期相对于基准值的差值
        int count = 0;
        int num = 0;
        int year = stoi(date.substr(0,4));
        int month = stoi(date.substr(5,2));
        int day = stoi(date.substr(8,2));
        
        for (int i=1970; i<year; i++) {
            if (is4Times(i)) {
                num++;
            }
        }
        for (int i=0; i<month; i++) {
            count = count+monthDay(year, i);
        }
        int temp = year-num-1970;
        count = count+num*366+temp*365+day;
        
        return count;
    }
public:
    int daysBetweenDates(string date1, string date2) {//求两个日期的差
        int count = 0;
        int day1=0,day2 = 0;
        day1 = countDays(date1);
        day2 = countDays(date2);
        count = abs(day1-day2);
        return count;
    }
};
```

------
👆是会做的分割线
对，下面都是我连题都没来得及看的部分

题先放下，我写完了就补题解（大概这两天，应该不咕吧。。）

### 5170. 验证二叉树(Medium)
####Problem Link

https://leetcode-cn.com/problems/validate-binary-tree-nodes/

#### Description
二叉树上有 n 个节点，按从 0 到 n - 1 编号，其中节点 i 的两个子节点分别是 `leftChild[i]` 和 `rightChild[i]`。

只有*所有*节点能够形成且*只*形成 一颗 有效的二叉树时，返回 `true`；否则返回 `false`。

如果节点 `i` 没有左子节点，那么 `leftChild[i]` 就等于 `-1`。右子节点也符合该规则。

注意：节点没有值，本问题中仅仅使用节点编号。

**示例1:**
```
0-->2-->3
|
|
v
1

输入：n = 4, leftChild = [1,-1,3,-1], rightChild = [2,-1,-1,-1]
输出：true
```
**示例2:**
```
0--->1
|    |
|    |
v    v
2--->3

输入：n = 4, leftChild = [1,-1,3,-1], rightChild = [2,3,-1,-1]
输出：false
```

**示例3:**
```
0<--->1

输入：n = 2, leftChild = [1,0], rightChild = [-1,-1]
输出：false
```
**示例4**
```
0-->1     3-->4
|         |
|         |
v         v
2         5

输入：n = 6, leftChild = [1,-1,-1,4,-1,-1], rightChild = [2,-1,-1,5,-1,-1]
输出：false
```
提示：

- 1 <= n <= 10^4
- length == rightChild.length == n
- -1 <= leftChild[i], rightChild[i] <= n - 1


#### Solution
```c++
class Solution {
public:
    bool validateBinaryTreeNodes(int n, vector<int>& leftChild, vector<int>& rightChild) {

    }
};
```

### 5171. 最接近的因数(Medium)
####Problem Link
https://leetcode-cn.com/problems/closest-divisors/

#### Description
给你一个整数 `num`，请你找出同时满足下面全部要求的两个整数：

  - 两数乘积等于  `num + 1` 或 `num + 2`
  - 以绝对差进行度量，两数大小最接近

你可以按任意顺序返回这两个整数。

**示例1:**
```
输入：num = 8
输出：[3,3]
解释：对于 num + 1 = 9，最接近的两个因数是 3 & 3；对于 num + 2 = 10, 最接近的两个因数是 2 & 5，因此返回 3 & 3 。
```
**示例2:**
```
输入：num = 123
输出：[5,25]
```

**示例3:**
```
输入：num = 999
输出：[40,25]
```

**提示**
- 1 <= num <= 10^9

#### Solution
```c++
class Solution {
public:
    vector<int> closestDivisors(int num) {

    }
};
```


### 碎碎念
这次周赛我就写出来一道题orz，不过也是第一次自己写题解的日子。害，自己真的很菜。觉得这周周赛比上周难一点，也可能是我脑子不太够用。有时候思路是有，但是要注意思路的可行性，然后后面注意一下时间复杂度什么的。下周加油～

---
title: Hot 100🔥 Day 2
categories: [Leetcode]
tags: [Hot100,Coding]
---

#### 写在最前

这个我没看是不是hot100的题，借这个分类记一下刷题笔记（好像是一个后端专题，专题所有内容都写在这一天了～

<!--more-->

### 459. 重复的子字符串

**Solution 1:** 枚举
通过`n'`和`n`的关系表示坐标的关系

假设原始的字符串是`s`，长度为`n`，重复的子字符串是`s'`，长度为`n'`
如果`s`由多个重复`s'`构成，则一定有：
- `n`是`n'`的倍数
- `s'`是`s`的前缀
- 对任意的`i`属于`[n', n)`，有`[i] = s[i-n]`

综上，n'之后的每个字符s[i]，都应该和它之前的`n'`个字符一一对应，即循环长度为`n'`。

又因为如果存在`s'`，则`s'`至少重复一次，所以我们寻找`n'`时只需要找前一半，即[1, n/2]


```java
import java.util.Scanner;

class solution459 {
    public static boolean repeatedSubstringPattern(String s) {
        int n = s.length();
        for (int i = 1; i <= n / 2; i++)
        {
            if (n % i == 0)
            {
                boolean match = true;
                for (int j = i; j < n; j++)
                {
                    if (s.charAt(j) != s.charAt(j - i))
                    {
                        match = false;
                        break;
                    }
                }
                if (match)
                {
                    return true;
                }
            }
        }
        return false;
    }

    public static void main(String[] args)
    {// main fuction
        Scanner input = new Scanner(System.in); //比较灵活的输入接受方式
        String s = input.nextLine();
        boolean result = repeatedSubstringPattern(s);
        System.out.println(result);
        input.close(); //最后输入需要关闭
    } 
}
```

**Solution 2:** 移位和换行

一个大佬非常秀的解法（醍醐灌顶！），思路如下：
设str = S + S，如果原始字符串由重复子串组成，则str去掉首尾字符之后仍能找到字符串S；反之，则原始字符串不包含重复子串（我没看懂大佬写的题解，所以不知道跟移位有什么关系，我回去再看几遍）。
  
```java
// 两行代码的写法
public boolean repeatedSubstringPattern(String s) {
    String str = s + s;
    return str.substring(1, str.length() - 1).contains(s);
}
```


### 1427.字符串的左右移

- 遍历指令数组，确定到底左移or右移
- 使用substring函数对数组进行整体的前后交换
    - 左移 -> (offset, n) + (0, n)
    - 右移 -> (n-offset, n) + (0, n-offset)

一开始想复杂了，不用一个字符一个字符的挪动，可以根据规律整体挪动。

```java
public class solution1427 {
    public String stringShift(String s, int[][] shift) {
        String str = "";
        int left = 0;
        int right = 0;
        int n = s.length();
        int offset = 0;
        for(int i = 0; i < shift.length; i++) {
            if(shift[i][0] == 0) {
                left += shift[i][1];
            } else if(shift[i][0] == 1) {
                right += shift[i][1];
            }
        }
        if (left > right) {
            offset = (left - right) % n;
            str = s.substring(offset, n) + s.substring(0, offset);
            return str;
        }else if (left < right) {
            offset = (right - left) % n;
            str = s.substring(n - offset, n) + s.substring(0, n - offset);
            return str;
        }else {
            return s;
        }
    }
    
    
}
```

#### 6. Z字形变换

通过二维矩阵模拟生成。
矩阵的行：numRows，

```java
public class solution6 {
    public static int upper(int a, int b) {
        if( a % b == 0){
            return a / b;
        } else {
            return a / b + 1;
        }
    }
    public static String convert(String s, int numRows) {
        int n = s.length();
        if (numRows == 1 || n <= numRows) {
            return s;
        }
        int nR = upper(n, numRows);
        int c = (numRows - 1) * nR;
        char[][] table = new char[numRows][(int)c]; // Construct 2-dimensional array
        int T = (numRows - 1) * 2;
        int x = 0; // row
        int y = 0; // column
        for (int i = 0; i < n; i++) {
            table[x][y] = s.charAt(i);
            if(i % T < numRows - 1) {
                x++; 
            } else {
                x--;
                y++;
            }
        }


        // append characters to string
        StringBuffer str = new StringBuffer();
        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j < c; j++) {
                if (table[i][j] != 0){
                    str.append(table[i][j]);
                }
            }
        }

        // Construct string
        String res = new String(str);
        return res;
    }

    public static void main(String args[]) {
        Scanner input = new Scanner(System.in);
        String s = input.nextLine();
        int numRows = input.nextInt();
        String str = convert(s, numRows);
        System.out.println(str);
        input.close();
    }
}

```
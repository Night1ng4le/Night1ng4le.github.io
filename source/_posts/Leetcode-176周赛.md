---
title: Leetcode-176周赛
categories: [Leetcode]
tags: [Week Contest]
---

### Link
https://leetcode-cn.com/contest/weekly-contest-176

### 5340. Count Negative Numbers in a Sorted Matrix
#### Description
Given a m * n matrix grid which is sorted in non-increasing order both row-wise and column-wise. 

<!--more-->

Return the number of negative numbers in grid.

**Example 1:**
```
Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
Output: 8
Explanation: There are 8 negatives number in the matrix.
```

**Example 2:**
```
Input: grid = [[3,2],[1,0]]
Output: 0
```

**Example 3:**
```
Input: grid = [[1,-1],[-1,-1]]
Output: 3
```

**Example 4:**
```
Input: grid = [[-1]]
Output: 1
```

**Constraints:**
> - m == grid.length
> - n == grid[i].length
> - 1 <= m, n <= 100
> - -100 <= grid[i][j] <= 100

#### Solution

我自己写周赛的时候用的是暴力循环的解法，因为最容易想，当时也没想着改进，不过显而易见，时间复杂度也比较高O(mn)。
**Version 1.0 暴力循环**
```c++
//Version 暴力解法
class Solution {
public:
    int countNegatives(vector<vector<int>>& grid) {
        int count = 0;
        for(int i=0;i<grid.size();i++){
            for (int j=0; j<grid[i].size(); j++) {
                if (grid[i][j]<0) {
                    count+=1;
                }
            }
        }
        return count;
    }
};
```

因为不满意O(mn)的时间复杂度，于是赛后我去啃了一下别人的思路，从易到难，逐步改进一下。

**Version 2.0 对行做二分查找**
因为数据是排好序的，自己有想过对行做二分查找降低复杂度，时间关系赛后反过来实现一下。这种策略的时间复杂度是O(mlogn)。
```c++
//binSearch
class Solution {
public:
       int countNegatives(vector<vector<int>>& grid){
        int count = 0, m = grid.size(), n = grid[0].size();
        for(int i=0;i<m;i++){
            vector<int> arr = grid[i];
            if (arr[n-1]>=0) {//整行非负，跳过
                continue;
            }
            if (arr[0]<0) {//第一个元素是负数，则整个矩阵是负数
                count += (m-i)*n;
                break;
            }
            int index = binSearch(arr);
            count = count+n-index;
        }
        return count;
    }

    //找第一个负数的下标
    int binSearch(vector<int>& arr){
        int left = 0;
        int right = arr.size();
        while (left < right) {
            int mid = left + (right-left)/2;
            if (arr[mid]>=0) {
                left = mid+1;
            }else{
                if (arr[mid-1]>=0) {//如果中点的前一个非负，说明找到了
                    return mid;
                }
                right = mid;
            }
        }
        return left;
    }
};
```

**Version 3.0 按对角线统计数据**
version2.0只利用到了行有序，并没有利用到列有序的特点，基于这个缺点，对上述方法提出改进，得到当前策略。因为矩阵的行列都是降序排序，所以我们从右上角出发，即grid[0][n-1]的位置，该点下面的点的值小于它，该点左侧的点的值大于它。所以这种策略的思路大致是：在每一层找一个这样的点，该点右侧均是负数。如果该层全是负数，则记为-1。从grid[0][n-1]的元素值开始，如果大于等于0，则终止，如果小于0，则左移一位，循环此过程。用变量记录每层第一个非正元素的位置，继续下一层。最后叠加次数，输出。

```c++
class Solution {
public:
    int countNegatives(vector<vector<int>>& grid) {
        int count = 0;
        int index = grid[0].size()-1;//从n-1开始
        for (int i=0; i<grid.size(); i++) {//按行循环
            for (int j = index; j>=0; j--) {//按列从右向左循环
                if (grid[i][j]>=0) {
                    index = j;
                    count += grid[0].size()-index-1;
                    break;
                }
                if (j==0) {//如果整行为负数，记为-1
                    index = -1;
                }
            }
            if (index==-1) {//单独计数整行负数的行
                count = count+grid[0].size();
            }
        }
        return count;
    }

};
```
Version 3.0的参考链接：https://leetcode-cn.com/problems/count-negative-numbers-in-a-sorted-matrix/solution/5340-tong-ji-you-xu-ju-zhen-zhong-de-fu-shu-by-blu/


### 5341. Product of the Last K Numbers

#### Description
Implement the class ProductOfNumbers that supports two methods:

1. `add(int num)`

	- Adds the number num to the back of the current list of numbers.

2. `getProduct(int k)`

    - Returns the product of the last k numbers in the current list.
    You can assume that always the current list has at least k numbers.

At any time, the product of any contiguous sequence of numbers will fit into a single 32-bit integer without overflowing.

 
**Example:**

> **Input**
> ["ProductOfNumbers","add","add","add","add","add","getProduct","getProduct","getProduct","add","getProduct"]
> [[],[3],[0],[2],[5],[4],[2],[3],[4],[8],[2]]
>
> **Output**
> [null,null,null,null,null,null,20,40,0,null,32]
>
> **Explanation**
> ProductOfNumbers productOfNumbers = new ProductOfNumbers();
> productOfNumbers.add(3);        // [3]
> productOfNumbers.add(0);        // [3,0]
> productOfNumbers.add(2);        // [3,0,2]
> productOfNumbers.add(5);        // [3,0,2,5]
> productOfNumbers.add(4);        // [3,0,2,5,4]
> productOfNumbers.getProduct(2); // return 20. The product of the last 2 numbers is 5 * 4 = 20
> productOfNumbers.getProduct(3); // return 40. The product of the last 3 numbers is 2 * 5 * 4 = 40
> productOfNumbers.getProduct(4); // return 0. The product of the last 4 numbers is 0 * 2 * 5 * 4 = 0
> productOfNumbers.add(8);        // [3,0,2,5,4,8]
> productOfNumbers.getProduct(2); // return 32. The product of the last 2 numbers is 4 * 8 = 32 

 

**Constraints:**

   - There will be at most 40000 operations considering both `add` and `getProduct`.
   - 0 <= num <= 100
   - 1 <= k <= 40000


#### Solution
**Version 1.0 暴力解法**
这个方法是我周赛自己搞的，本来没想着能过，结果还是那句话，cn版卡的不太严，所以就神奇的通过了orz。很显然这不是一个好方法，因为连续的非零乘法运算积会非常大，每一步也会用更久的时间，所以这个方法虽然能通过，但是不可取。当时觉得太久了，就想有没有改进的乘法运算，不过我没有这方面的知识储备，也没查到相关资料。
```c++
//暴力解法
class ProductOfNumbers {
private:
    int result;
    int arr[40000];
    int size;
public:
    ProductOfNumbers() {
        size = 0;
    }
    
    void add(int num) {
        arr[size] = num;
        size+=1;
    }
    
    int getProduct(int k) {
        if (size<k) {
            return -1;
        }
        result = 1;
        for (int i=0; i<k; i++) {
            if (result==0) {
                return 0;
            }
            result = (arr[size-i-1]*result);
        }
        return result;
    }
};
```
**Version 2.0 前缀积**

这个方法是我赛后看来的，时间复杂度为O(1)，不过我没怎么看懂，等我看懂了再补笔记。
```c++
//前缀积
class ProductOfNumbers {
    public:
    int mult[40010],isZeroPos,n;//前缀连乘积(且把0视为1)
    ProductOfNumbers() {
        n = 0;//当前添加的数的下标
        isZeroPos = 0;//若包含该下标 则连乘积为0
        mult[0] = 1;
    }
    void add(int num) {
        ++n;
        if(num == 0) 
            isZeroPos = n, mult[n] = 1;//更新0点,因为该点对后面的数的乘积无影响故令此处连乘积为 1
        else mult[n] = mult[n-1]*num; 
    }
    int getProduct(int k) {
        k = n-k+1;//也就是从前往后数的第n-k+1个数
        if(k <= isZeroPos) return 0;//包含了0 所以连乘积一定为0
        else return mult[n]/mult[k-1];//若不包含0 则为k~n的连乘积=1~n的连乘积/1~k-1的连乘积
    }
};

/**
 * Your ProductOfNumbers object will be instantiated and called as such:
 * ProductOfNumbers* obj = new ProductOfNumbers();
 * obj->add(num);
 * int param_2 = obj->getProduct(k);
 */
```



### 小结
这周周赛做出两道题，比起来上一周多ac了一道（可能是因为这周的第二题能暴力解决orz），也算是有一丢丢进步。周赛里复习了vector的相关用法、二分查找，也学会了一点新的思路，后面两道题我也会做，但是不会放在周赛小结里了，会单独拎出来做明白。这周周赛的感觉是简单题的意义在于寻找更好的策略。以后遇到问题，需要注意的是，在规定时间里是否有解？如果有，自己是否能写出最优解？镜子会继续加油的～❤
p.s:暴力虽然很丑，但有用！

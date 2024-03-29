---
title: Leetcode - Remove Duplicates from Sorted Array
categories: [Leetcode]
tags: [Array]
---
### Problem link
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/

### Description
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

<!-- more -->

**Example 1:**
```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**
```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**
```
Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.
 
Internally you can think of this:

// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);
 
// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
 for (int i = 0; i < len; i++) {
     print(nums[i]);
 }
```

**说明:**
为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**“引用”**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

> // nums是以“引用”方式传递的。也就是说，不对实参做任何拷贝
> int len = removeDuplicates(nums);
> // 在函数里修改输入数组对于调用者是可见的。
> // 根据你的函数返回的长度, 它会打印出数组中`该长度范围内`的所有元素。
```
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```



### Solution
``` c++
//记录思路：
//设置count作为计数器，统计数组不重复的元素个数
//首元素必定不重复，所以循环从第二个元素开始
//如果两个元素不同，计数器+1，如果两个元素相同，则做赋值

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty()){
            return 0;
        }
        int count = 0;
        for(int i=1; i<nums.size(); i++){
            if(nums[count] != nums[i]){
                count++;
                nums[count] = nums[i];
            }
        }
        return count+1; 
    }
};
```

### 碎碎念
很久没有写代码了，结果入门这种坑脑子都会像生锈一样orz


---
title: Hot 100🔥 Day 3
categories: [Leetcode]
tags: [hot100,coding,Array]
---

#### 11. 盛水最多的容器

[Problem](https://leetcode.cn/problems/container-with-most-water/)
<!--more-->

##### 朴素的暴力解法

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        // initialization
        int maxVol = 0;
        int temp = 0; 
        // brute force
        for (int i = 0; i < height.size()-1; i++) {
            for(int j = i+1; j < height.size(); j++) {
                temp = min(height[i], height[j]) * (j-i);
                maxVol = (maxVol < temp) ? temp : maxVol; 
            }
        }
        return maxVol;
    }
};
```

##### 双指针

矩形面积S = h * w；
h = min(height[left], height[right])
w = right - left;

初始时两个指针分别指向0和height.size()-1的位置，无论移动哪个指针，矩形的宽都会-1，因此有：
- 如果移动后h变大，则面积**可能增加**；
- 如果移动后h减小，则面积**一定减小**。

每次height较小的指针，用于更新height。

**时间复杂度：** O(N)，双指针一共遍历一次数组。
**空间复杂度：** O(1)，l、r、maxVol使用常数空间

```c++
class Solution {
public:
    int maxArea(vector<int>& height) { // Two pointers
        // initialization
        int l = 0; //left pointer
        int r = height.size() - 1; // right pointer
        int h= min(height[r], height[l]);
        int maxVol = (r - l) * h;
        while(l < r) {// end condition
            if(height[l]<height[r]){ //each time move the shorter one
                l++;
            }else {
                r--;
            }
            h = min(height[r],height[l]);
            maxVol = maxVol >= (r - l) * h? maxVol : (r - l) * h;
        }
        return maxVol;
    }
};
```

#### 15. 三数之和

[Problem](https://leetcode.cn/problems/3sum/)

注：返回值是三元组对应位置的值，而且输出顺序不重要 -> 是可以考虑排序的解法(不可以包含重复的三元组)


##### 排序 + 双指针


> 题解思路（我自己没想出来）：
1. 特殊解，对于数组长度`n<3`或者`n==null`的时候，直接返回[]
2. 对数组进行排序（从小到大）
3. 遍历排序后的数组
	- 若nums[i]>0，后面不可能有三个数相加和等于0，直接返回结果。
	- 对于重复元素：跳过，避免出现重复解。
	- left = i+1，right = n-1，当left < right时，执行循环：
		- 当nums[i] + nums[left] + nums[right] == 0，执行循环，判断左右界限是否和下一位置重复，去除重复解。将left和right移至下一个位置，寻找新的解。
		- 若和大于0，说明nums[right]太大，right左移
		- 若和小于0，说明nums[left]太小，left右移

**复杂度分析：**
- 时间复杂度：O(n^2)，数组排序O(NlogN)，遍历数组O(n)，双指针遍历O(n)，总体`O(NlogN)+O(n)*O(n)`
- 空间复杂度：O(1)，

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
    	// Initialize
    	int n = nums.size();
    	vector<vector<int>> res;

    	// if n < 3, return empty vector
    	if (n < 3)
    	{
    		return {};
    	}

    	// Sort array
    	sort(nums.begin(), nums.end());
    	for (int left = 0; left < n; left++) {
    		if(nums[left] > 0) return res; // 递增顺序，left对应的值大于0，则不可能相加为0
    		
    		// move repeated number
    		if(left > 0 && nums[left] == nums[left-1]) {
    			continue;
    		}

    		int target = -nums[left];
    		int right = n - 1;
    		// find second
    		for(int mid = left + 1; mid < n; mid++) {
    			// remove repeated
    			if(mid > left + 1 && nums[mid] == nums[mid-1]) {
    				continue;
    			}
    			while (mid < right && nums[mid] + nums[right] > target) {
    				right--;
    			}
    			if(mid == right) {
    				break;
    			}
    			if (nums[mid] + nums[right] == target) {
    				res.push_back({nums[left], nums[mid], nums[right]});
    			}
    		}
    	}
    	return res;
    }
    
};
```

some note:
```c++
void push_back (const value_type& val);

void push_back (value_type&& val);
// Adds a new element at the end of the vector, after its current last element. 

// 返回一个空的vector；
return {};  // c++ 11
// or
return vector<int>(); // general method


// sort
sort(begin_index, end_index); 
```

#### 31. 下一个排列

[题目](https://leetcode.cn/problems/next-permutation/?favorite=2cktkvj)

提到了字典序（我都不知道这玩意是啥），



#### 33. 搜索旋转排序数组
[题目]()










后面打算长期使用c++了，我发现我无法放弃这个让我又爱又恨的语言。
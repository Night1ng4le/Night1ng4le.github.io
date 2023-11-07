---
title: Leetcode - 912. sortArray
categories: [Leetcode]
tags: [Stack,Algorithm Training]
---



<!--more-->

```c++
//BuubleSort
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        for(int i=0; i<nums.size()-1; i++){
            for(int j=0; j<nums.size()-1; j++){
                if (nums[j]>nums[j+1]) {
                    int temp = nums[j];
                    nums[j] = nums[j+1];
                    nums[j+1] = temp;
                }
            }
        }
        return nums;
    }
};
```

```c++
//MergeSort
class Solution {
public:
    void merge(vector<int>&nums, vector<int> temp, int low, int high, int mid){
        for(int k=low;k<=high;k++) {
                temp[k] = nums[k];
        }
        int i = low, j = mid+1;
        for(int k=low;k<=high;k++) {
            if(i>mid) nums[k] = temp[j++];
            else if(j>high) nums[k] = temp[i++];
            else if(temp[j]<temp[i]) {
                nums[k] = temp[j++];
            }
            else nums[k] = temp[i++];
        }
    }
    void sortarray(vector<int>&nums, vector<int> temp, int low, int high){
        if(high<=low) return;
        int mid = (low+high)/2;
        if(nums[mid] < nums[mid+1]) return;
        sortarray(nums,temp,low,mid);
        sortarray(nums,temp,mid+1,high);
        if (nums[mid+1]<nums[mid]) {
            return;
        }
        merge(nums,temp,low,high,mid);

    }

    vector<int> sortArray(vector<int>& nums) {
        vector<int> temp = nums;
        sortarray(nums,temp,0,int(nums.size()-1));
        return nums;
    }

};

```

```c++
//Mergesort version 2.0
class Solution {
public:
    vector<int> t;  // 临时排序的数的，然后在合并回原数组
    
    void merge(vector<int>& nums, int l, int mid, int r) {
        int i = l, j = mid + 1;
        int len = 0;
        
        while (i <= mid && j <= r) {
            if (nums[i] <= nums[j]) t[len++] = nums[i++];
            else t[len++] = nums[j++];
        }
        while (i <= mid) t[len++] = nums[i++];
        while (j <= r) t[len++] = nums[j++];
        
        for (int i = 0; i < len; i++) {
            nums[l+i] = t[i];
        }
    }
    
    void mergeSort(vector<int>& nums, int l, int r) {
        if (l >= r) return;
        int mid = l + r >> 1;
        mergeSort(nums, l, mid);
        mergeSort(nums, mid + 1, r);
        merge(nums, l, mid, r);
    }
    
    vector<int> sortArray(vector<int>& nums) {
        int n = nums.size();
        t = vector<int>(n);
        mergeSort(nums, 0, n - 1);
        return nums;
    }
};

```
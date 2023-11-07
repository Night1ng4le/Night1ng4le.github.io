---
title: Hot 100🔥 Day 1
categories: [Leetcode]
tags: [hot100,coding]
---

因为个人原因，开始Leetcode刷题之路，第一个小目标，先把Hot 100刷完一轮。（先立个flag，希望不要变成戏台上的老将军）
主要涉及Java和c++，和github仓库里的leetcode_note侧重点不太一样。

<!--more-->

### 0x01 两数之和


vector：详见Manual，注意c++中vector的引用格式

#### BruteForce

```java
// Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        for (int i = 0; i < nums.length; i++) {
			for(int j = i + 1; j < nums.length; j++) { // notice: i != j
				if (nums[i] + nums[j] == target){
                    res[0] = i;
                    res[1] = j;
					break;
				}
			}
		}
        return res; //直接返回数组名称
    }
}
```

```c++
// C++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) 
	{
		vector<int> res(2);
		for (int i = 0; i < nums.size(); i++)
		{
			for (int j = i + 1; j < nums.size(); j++)
			{
				if (nums[i] + nums[j] == target)
				{
					res[0] = i;
					res[1] = j;
				}
			}
		}
		return res;
	}
};
```


#### HashTable

HashMap：详见Manual

注意问题转换，碎碎念版本在[Github](https://github.com/Night1ng4le/leetcode-note/blob/main/DS-basic/1-two-sum.md)。

```java
// Java
class Solution {
	public int[] twoSum(int[] nums, int target)
	{
		Map<Integer, Integer> map = new HashMap<Integer, Integer>();
		for (int i = 0; i < nums.length; i++) 
		{
			if(map.containsKey(target - nums[i])) {
				return new int[]{map.get(target - nums[i]), i}; // notice return approach
			}
            map.put(nums[i],i);
		}
		return new int[0];
	}
}
```

```c++
// C++
class Solution {
	vector<int> twoSum(vector<int>& nums, int target) 
	{
		map<int, int> hashtable;
		for (int i = 0; i < nums.size(); ++i)
		{
			if (hashtable.find(target - nums[i])) 
			{
				
			}
			hashtable.
		}
	}
};
```

### 0x02 两数相加

Java空指针 - `nullptr`

是一个模拟，不难但需要注意细节。
- 进位flag记录之后要刷新val和flag的值
- 循环终止条件是两个链表都空
- 单链表空时，其值记为0
- 最后一个数字要判断是否有进位

```java
// Java
class Solution {
	public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
		// Initialization
		boolean flag = false;
		ListNode first = new ListNode(0);
		ListNode node = first; // node as a pointers
		int v1 = 0;
		int v2 = 0;

		// 
		while (l1 || l2)
		{
			// check v1 & v2 value
			v1 = l1 ? l1.val : 0;
			v2 = l2 ? l2.val : 0;
			//
			if (l1) {
				l1 = l1.next;
			}
			if (l2) {
				l2 = l2.next;
			}

			// sum
			node.val = flag ? (v1 + v2 + 1) : (v1 + v2);
			flag = false; // update flag

			//update value
			if (node.val >= 10) {
				flag = true;
				node.val %= 10;
			}

			if (l1 || l2) {
				ListNode next = new ListNode(); // default val = 0
				node.next = next;
				node = next;
			}

		}
		// update last flag number
		if (flag) {
			ListNode next = new ListNode(1);
			node.next = next;
		}
		return first;
	}
}
```

链表c++我不熟，晚点补
```c++
// C++ 
```

### 0x03 无重复字符最长子串


### 0x04 寻找两个正序数组的中位数
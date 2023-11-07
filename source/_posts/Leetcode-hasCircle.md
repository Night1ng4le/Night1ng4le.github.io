---
title: Leetcode-141.Linked List Cycle
categories: [Leetcode]
tags: [Data Structure,Linked List]
---

### Problem Link
https://leetcode-cn.com/explore/learn/card/linked-list/194/two-pointer-technique/744/

### Description
Given a linked list, determine if it has a cycle in it.

<!--more-->

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

**Example 1:**
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.

3 --> 2 --> 0 --> 4
      ^           |
      |           |
       -----------
```


**Example 2:**
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.

1 --> 2
^     |
|     |
 -----

```

**Example 3:**
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.

1

```


### Solution
>想象一下，有两个速度不同的跑步者。如果他们在直路上行驶，快跑者将首先到达目的地。但是，如果它们在圆形跑道上跑步，那么快跑者如果继续跑步就会追上慢跑者。
>
>这正是我们在链表中使用两个速度不同的指针时会遇到的情况：
>
>   `1.如果没有环，快指针将停在链表的末尾。`
>   `2.如果有环，快指针最终将与慢指针相遇。`
>所以剩下的问题是：这两个指针的适当速度应该是多少？
>一个安全的选择是每次移动慢指针`一步`，而移动快指针`两步`。每一次迭代，快速指针将额外移动一步。如果环的长度为 M，经过 M 次迭代后，快指针肯定会多绕环一周，并赶上慢指针。
> —— From Leetcode

根据上述思路，得到如下解法：


```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(head==NULL || head->next==NULL){
            return false;//如果链表为空或只有一个节点，没有环
        }
        ListNode* SNode = head;
        ListNode* FNode = head->next;
        while(SNode!=FNode){
            if(FNode==NULL || FNode->next==NULL){ //快指针停在链表末尾，没有环
                return false;
            }
            SNode = SNode->next;// 慢指针走一步
            FNode = FNode->next->next;//快指针走两步
        }
        return true;
    }
};
```


#### 写在最后
我自己觉得链表是我的一个弱点，学的迷迷糊糊的，嘤～还是需要多看一看链表相关的题目和题解吧，基础太差了总会写出来一些奇怪的东西。加油呀～❤
---
title: LinkedList - Leetcode链表专项
categories: [Leetcode]
tags: [Data structure] 
---

终于想起来我还有个blog，刚好最近在刷题，所以随手记一下方便二刷～
祝自己食用愉快！

写在最前：链表题不出意外的话，通常要设置一个隐藏头节点，便于操作。

<!--more-->

[TOC]

## 双指针

这种一般是需要快慢指针的情况，通常情况下快指针一次移动2 steps，慢指针一次移动1 step。我感觉双指针的题半数考察的是两个指针之间的数学关系。如果对数学关系比较敏感，这个部分还是没那么难掌握的。

### 环形链表


### 环形链表II


### 相交链表


### 删除链表的倒数第N个节点


## 链表经典问题

### 反转链表

**题目描述**：https://leetcode.cn/problems/reverse-linked-list/

#### 辅助栈

这个思路是我看见反转的第一反应，也不知道为什么这么喜欢辅助栈。大概思路就是把每个节点的值都存进栈里，然后再从栈顶一个一个连回来。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        Stack<Integer> temp = new Stack();
        while(head!=null&&head.next!=null){
            temp.push(head.val);
            head = head.next;
        }
        if(head!=null){
            ListNode first = head;
            while(!temp.isEmpty()){
                ListNode next = new ListNode(temp.pop());
                first.next = next;
                first = first.next;
            }
        }
        return head;
    }
```
时间复杂度O(n)，需要遍历时间链表两次
空间复杂度O(n)，因为需要建立一个辅助栈


#### 迭代

- prev表示curr前一个节点，
- next表示curr后一个节点
- curr表示当前节点

一个非常经典且精简的思路，可惜我是个麻瓜。
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        ListNode next;
        while(curr!=null){
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

### 移除链表元素

**题目描述：** https://leetcode.cn/problems/remove-linked-list-elements/

写了两天乱七八糟的东西，滚回来写代码的时候有点懵。

#### 递归

链表本身的结构跟递归算法的思路类似，所以感觉可以用这个方法写
```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head==null){
            return head;
        }
        head.next = removeElements(head.next,val);
        return head.val==val?head.next:head;
    }
}
```

#### 迭代

链表常规做法， 先在头部加一个隐藏节点first。

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode first = new ListNode();
        first.next = head;
        ListNode temp = first;
        while(temp!=null&&temp.next!=null){
            if(temp.next.val==val){
                temp.next = temp.next.next;
            }else{
                temp = temp.next;
            }
        }
        return first.next;
    }
}
```


### 奇偶链表


### 回文链表
---
title: Tree
categories: [Leetcode]
tags: [Data Structure]
---


### 二叉树的遍历
**遍历：**按照`特定次序`访问节点，每个节点`恰好`被访问一次。
$$T = V ∪ L ∪ R$$

**分类**
先序：V|L|R
中序：L|V|R
后序：L|R|V
层次遍历
`注：除层次遍历外，其他的分类取决于根节点的遍历顺序，在遍历子树时，顺序一直是先左后右。`

<!--more-->

> 无论各种递归式遍历算法还是各种迭代式遍历算法，都只需要渐进的线性时间；而且相对而言，前者更加简明。递归版遍历算法时间、空间复杂度的常系数，相对于迭代版更大。同时从学习的角度来看，从底层实现迭代式遍历，也是加深对相关过程和技巧理解的有效途径。              ——《数据结构（第3版）》，邓俊辉


### 前序遍历
#### 递归
递归版比较容易实现，因为先序遍历的思路本身就是递归的。先遍历根节点，进而遍历左子树，进而遍历右子树。
```c++
/*
struct TreeNode{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x):val(x),left(NULL),right(NULL){}
    };
*/

class Solution {
public:
    vector<int> visit;
    vector<int> preorderTraversal(TreeNode* root) {
        if (root!=NULL) {
            visit.push_back(root->val);
            preorderTraversal(root->left);
            preorderTraversal(root->right);
        }
        return visit;
    }
};
```

#### 迭代
上述递归是一个典型的尾递归，所以很好转化为迭代的算法。这里借助辅助栈，需要注意的是，由于栈后进先出的特性，元素入栈顺序是先右后左。
```c++
//Version 1.0
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> S;
        vector<int> visit;
        if (root!=NULL) S.push(root);
        while (!S.empty()) {
            root = S.top();
            S.pop();
            visit.push_back(root->val);

            //子树入栈顺序先右后左
            if (root->right!=NULL) {
                S.push(root->right);
            }
            if (root->left!=NULL) {
                S.push(root->left);
            }
        }
        return visit;
    }
};

```
版本一非常简明，但是并不容易推广到非尾递归的中序甚至后序遍历。所以需要换一个新的思路。

观察一个规模比较大的树，发现先序遍历起始于树根，沿左侧孩子分支持续下行。所以得到新思路：
> 1) 自顶而下地依次访问左侧链的沿途节点
> 2) 自底而上地遍历各层的每一棵右子树

```c++
//Version 2.0
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> S;
        vector<int> visit;
        while (true) {
			// visitAlongLeftBranch();
            while (root) {
                visit.push_back(root->val);
                S.push(root->right);
                root = root->left;
            } 
            if (S.empty()) {
                break;
            }
            root = S.top();
            S.pop();
        }
        return visit;
    }
    
};
```


### 中序遍历
#### 递归
参考先序递归的写法，中序的递归并不难写出来。
```c++
class Solution {
public:
    vector<int> visit;
    vector<int> inorderTraversal(TreeNode* root) {
        if (root!=NULL) {
            inorderTraversal(root->left);
            visit.push_back(root->val);
            inorderTraversal(root->right);
        }
        return visit;
    }
};
```

#### 迭代
```c++
class Solution {
public:
    vector<int> visit;
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> S;
        while (true) {
//            visitAlongLeftBranch(root, S);
            while (root) {
                S.push(root);
                root = root->left;
            }
            if (S.empty()) {
                break;
            }
            root = S.top();
            S.pop();
            visit.push_back(root->val);
            root = root->right;
            
        }
        return visit;
    }

};

```

### 后序遍历
#### 递归
```c++
class Solution {
public:
    vector<int> visit;
    vector<int> postorderTraversal(TreeNode* root) {
        if (root!=NULL) {
            postorderTraversal(root->left);
            postorderTraversal(root->right);
            visit.push_back(root->val);
        }
        return visit;
    }
};
```
#### 迭代
这里是两个辅助栈的版本。这里的思路是这样的，stack2的作用是纯粹的辅助输出，利用栈后进先出的特性。需要注意的是，这里push(node)等操作，一定要注意判断指针不为空。
```c++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> S1;
        stack<int> S2;
        vector<int> res;
        S1.push(root);
        while (!S1.empty()) {
            TreeNode* node = S1.top();
            S1.pop();
            if(node){//注意这里，一定要保证node本身是非空的，增加代码的健壮性
                S2.push(node->val);
                if (node->left!=NULL) {
                    S1.push(node->left);
                }
                if (node->right!=NULL) {
                    S1.push(node->right);
                }
            }
            
        }
        while (!S2.empty()) {
            res.push_back(S2.top());
            S2.pop();
        }
        
        return res;
    }
};

```


### 参考链接
[《数据结构》- 邓俊辉]()





---
layout: post
comments: true
categories: Algorithm
tag : 알고리즘
---

## LeetCode - Symmetric Tree

- Null 포인터 전달에 대해 조금 더 신경 써야 하는 문제!
- 재귀를 이용하여 간단하게 문제 해결 가능~

###### 보완할 수 있는 점

- 재귀 말고 bfs를 이용해서도 문제 해결 가능

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        return go(root->left, root->right);
    }
    bool go(TreeNode * node1, TreeNode * node2){
        if(node1==NULL && node2 == NULL) return true;
        if(node1==NULL || node2 == NULL) return false;
        if(node1->val != node2->val) return false;
        return (go(node1->left, node2->right) && go(node1->right, node2->left));
    }
};
```
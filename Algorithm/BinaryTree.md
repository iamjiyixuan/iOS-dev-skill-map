# Binary Tree 二叉树
<!-- TOC -->

- [1. TreeNode](#1-treenode)
- [2. Preorder Traversal 前序遍历](#2-preorder-traversal-前序遍历)
- [3. Inorder Traversal 中序遍历](#3-inorder-traversal-中序遍历)
- [4. Postorder Traversal 后序遍历](#4-postorder-traversal-后序遍历)
- [5. Level Order Traversal 层次遍历](#5-level-order-traversal-层次遍历)
- [6. MaxDepth 计算最大深度](#6-maxdepth-计算最大深度)
- [7. MinDepth 计算最小深度](#7-mindepth-计算最小深度)
- [8. Invert 翻转](#8-invert-翻转)
- [9. IsSameTree 判等](#9-issametree-判等)
- [10. IsSymmetric 判断是否对称](#10-issymmetric-判断是否对称)
- [11. IsBalanced 判断是否平衡](#11-isbalanced-判断是否平衡)
- [12. Binary Search Tree (BST) 二叉搜索树](#12-binary-search-tree-bst-二叉搜索树)
    - [12.1. IsValidBST](#121-isvalidbst)
    - [12.2. TrimBST](#122-trimbst)
- [13. Depth-First-Search (DFS) 深度优先搜索算法](#13-depth-first-search-dfs-深度优先搜索算法)
- [14. Breadth-First-Search (BFS) 广度优先搜索算法](#14-breadth-first-search-bfs-广度优先搜索算法)

<!-- /TOC -->

## 1. TreeNode
``` C
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};
```

## 2. Preorder Traversal 前序遍历

## 3. Inorder Traversal 中序遍历
Ref: [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* inorderTraversal(struct TreeNode* root, int* returnSize) {
    
}
```

## 4. Postorder Traversal 后序遍历

## 5. Level Order Traversal 层次遍历
``` C
int** levelOrder(struct TreeNode* root, int** columnSizes, int* returnSize) {
    
}
```

## 6. MaxDepth 计算最大深度
Ref: [LeetCode 104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
int maxDepth(struct TreeNode* root) {
    if (root) {
        int leftMaxDepth = maxDepth(root->left);
        int rightMaxDepth = maxDepth(root->right);
        if (leftMaxDepth >= rightMaxDepth) {
            return leftMaxDepth + 1;
        } else {
            return rightMaxDepth + 1;
        }
    }
    return 0;
}
```

## 7. MinDepth 计算最小深度

## 8. Invert 翻转
Ref: [LeetCode 226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
struct TreeNode* invertTree(struct TreeNode* root) {
    if (root) {
        struct TreeNode *temp = root->left;
        root->left = invertTree(root->right);
        root->right = invertTree(temp);
    }
    return root;
}
```

## 9. IsSameTree 判等
Ref: [LeetCode 100. Same Tree](https://leetcode.com/problems/same-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool isSameTree(struct TreeNode* p, struct TreeNode* q) {
    if (!p && q) return false;
    if (p && !q) return false;
    if (!p && !q) return true;
    
    if (p->val != q->val) return false;
    if (!isSameTree(p->left, q->left)) return false;
    if (!isSameTree(p->right, q->right)) return false;
    
    return true;
}
```

## 10. IsSymmetric 判断是否对称
Ref: [LeetCode 101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool isLeaf(struct TreeNode* node) {
    if (!node) return true; 
    if (!node->left && !node->right) return true;
    return false;
}

bool isMirror(struct TreeNode* node1, struct TreeNode* node2) {
    if (node1 && !node2) return false;
    if (!node1 && node2) return false;
    if (!node1 && !node2) return true;
    if (node1->val != node2->val) return false;
    if (isLeaf(node1) && isLeaf(node2) && node1->val == node2->val) return true;
    
    return isMirror(node1->left, node2->right) && isMirror(node1->right, node2->left); 
}

bool isSymmetric(struct TreeNode* root) {
    if (!root) return true;
    return isMirror(root->left, root->right);
}
```

## 11. IsBalanced 判断是否平衡

> a height-balanced binary tree is defined as: a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Ref: [LeetCode 110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool isBalanced(struct TreeNode* root) {
    
}
```

## 12. Binary Search Tree (BST) 二叉搜索树

### 12.1. IsValidBST
Ref: [LeetCode 98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)
``` C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool isValidBST(struct TreeNode* root) {
    
}
```

### 12.2. TrimBST
Ref: [LeetCode 669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/description/)
``` C
```

## 13. Depth-First-Search (DFS) 深度优先搜索算法
...

## 14. Breadth-First-Search (BFS) 广度优先搜索算法
...
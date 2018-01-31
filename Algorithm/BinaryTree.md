# Binary Tree 二叉树

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

## 4. Postorder Traversal 后序遍历

## 5. Level Order Traversal 层次遍历
``` C
int** levelOrder(struct TreeNode* root, int** columnSizes, int* returnSize) {
    
}
```

## 6. MaxDepth 计算最大深度
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

## 9. 判断是否平衡

## 10. IsSymmetric 判断是否对称
``` C
bool isSymmetric(struct TreeNode* root) {

}
```
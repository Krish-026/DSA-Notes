#30-03-2023 




Given[[Binary Tree Maximum Path Sum]] a binary tree, determine if it is **height-balanced**.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

**Input:** root = `[3,9,20,null,null,15,7]`
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

**Input:** root = `[1,2,2,3,3,null,null,4,4]`
**Output:** false

**Example 3:**

**Input:** root = []
**Output:** true

**Constraints:**

-   The number of nodes in the tree is in the range `[0, 5000]`.
-   `-104 <= Node.val <= 104`




```cpp
class Solution {
    int height(TreeNode* root){
        if(!root) return 0;
        int l = height(root->left);
        if(l == -1) return l;
        int r = height(root->right);
        if(r == -1) return r;
        if(abs(l-r) > 1) return -1;
        return max(l, r) + 1;
    }
public:
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        int ans = height(root);
        if(ans == -1) return false;
        return true;
    }
};
```
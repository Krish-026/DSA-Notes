#30-03-2023 

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = `[1,2,3,4,5]`
**Output:** 3
**Explanation:** 3 is the length of the path `[4,2,1,3]` or `[5,2,1,3]`.

**Example 2:**

**Input:** root = `[1,2]`
**Output:** 1

**Constraints:**

-   The number of nodes in the tree is in the range `[1, 104]`.
-   `-100 <= Node.val <= 100`

```cpp
class Solution {
private: 
    int height(TreeNode* root, int& sum){
        if(!root) return 0;
        int L = height(root->left, sum);
        int R = height(root->right, sum);
        sum = max(L + R, sum);
        return max(L, R) + 1;
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        if(!root) return 0;
        int ans = 0;
        int h =height(root, ans) - 1;
        return ans;
    }
};
```
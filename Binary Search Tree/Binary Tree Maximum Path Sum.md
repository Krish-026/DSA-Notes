
#30-03-2023 


A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

**Input:** root = `[1,2,3]`
**Output:** 6
**Explanation:** The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

**Input:** root = `[-10,9,20,null,null,15,7]`
**Output:** 42
**Explanation:** The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.


## Approach

```cpp
class Solution {
private:
    int height(TreeNode* root, int& sum){
        if(!root) return 0;
        int lsum = height(root->left, sum);
        if(lsum < 0) lsum = 0;
        int rsum = height(root->right, sum);
        if(rsum < 0) rsum = 0;
        sum = max(sum, lsum+rsum+root->val);
        return max(lsum, rsum) + root->val;
    }
public:
    int maxPathSum(TreeNode* root) {
        int sum = INT_MIN;
        // Given atleast 1 root
        height(root, sum);
        return sum;
    }
};
```
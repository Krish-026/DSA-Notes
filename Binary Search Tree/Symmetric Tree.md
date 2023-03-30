
#CST101-29-03-2023 
#29-03-2023 

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

**Input:** root = [1,2,2,3,4,4,3]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

**Input:** root = [1,2,2,null,3,null,3]
**Output:** false

**Constraints:**

-   The number of nodes in the tree is in the range `[1, 1000]`.
-   `-100 <= Node.val <= 100`


## Approach 1 :

```cpp
class Solution {
    bool ans(TreeNode* L, TreeNode* R){
        if(L == NULL and R == NULL)
            return true;
        if(L == NULL or R == NULL)
            return false;
        if(L->val != R->val)
            return false;
        return ans(L->left, R->right) and ans(L->right, R->left);        
    }
public:
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        return ans(root->left, root->right);
    }
};
```

## Another Approach

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        queue<TreeNode*>q;
        q.push(root->left);
        q.push(root->right);
        while(!q.empty()){
            TreeNode* L = q.front(); q.pop();
            TreeNode* R = q.front(); q.pop();
            if(!L and !R) continue;
            if(!L or !R) return false;
            if(L->val != R->val) return false;
            q.push(L->left);
            q.push(R->right);
            q.push(L->right);
            q.push(R->left);
        }
        return true;
    }
};
```

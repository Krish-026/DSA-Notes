#30-03-2023 



Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = `[3,9,20,null,null,15,7]`
**Output:**` [[3],[20,9],[15,7]]`

**Example 2:**

**Input:** root = `[1]`
**Output:** `[[1]]`

**Example 3:**

**Input:** root = `[]`
**Output:** `[]`

**Constraints:**

-   The number of nodes in the tree is in the range `[0, 2000]`.
-   `-100 <= Node.val <= 100`


## Approach


```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>>ans;
        if(!root) return ans;
        queue<TreeNode*>q;
        q.push(root);
        bool reverse = false;
        while(!q.empty()){
            size_t size = q.size();
            vector<int>arr(size);
            for(int i = 0; i < size; ++i){
                TreeNode* temp = q.front(); q.pop();    
                int index = reverse ? (size - 1 - i) : i ;
                arr[index] = temp->val;
                if(temp->left) q.push(temp->left);
                if(temp->right) q.push(temp->right);
            }
            ans.push_back(arr);
            reverse = !reverse;
        }
        return ans;
    }
};
```
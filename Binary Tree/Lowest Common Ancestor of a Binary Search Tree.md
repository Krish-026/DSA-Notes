#CST101-06-04-2023 
#06-04-2023 


Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = `[6,2,8,0,4,7,9,null,null,3,5],` p = 2, q = 8
**Output:** 6
**Explanation:** The LCA of nodes 2 and 8 is 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = `[6,2,8,0,4,7,9,null,null,3,5]`, p = 2, q = 4
**Output:** 2
**Explanation:** The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

**Example 3:**

**Input:** root = `[2,1]`, p = 2, q = 1
**Output:** 2

**Constraints:**

-   The number of nodes in the tree is in the range `[2, 105]`.
-   `-109 <= Node.val <= 109`
-   All `Node.val` are **unique**.
-   `p != q`
-   `p` and `q` will exist in the BST.



```cpp
class Solution {
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
private:
    TreeNode* dfs(TreeNode* root, TreeNode* p, TreeNode* q){
        if(!root) return root;
        if(root->val > p->val and root->val > q->val)
            return dfs(root->left, p, q);
        else if(root->val < p->val and root->val < q->val)
            return dfs(root->right, p, q);
        else return root;
    }
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return NULL;
        return dfs(root, p, q);
    }
};
```



```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return NULL;
        while(1){
            if(root->val > p->val and root->val > q->val)
                root = root->left;
            else if(root->val < p->val and root->val < q->val)
                root = root->right;
            else return root;
        }
        return NULL;
    }
};
```



```cpp
class Solution {
public:
    Node* connect(Node* root){
        if(!root) return root;
        Node* left = root;
        while(left->left){
            Node* cur = left;
            while(cur){
                cur->left->next = cur->right;
                if(cur->next){
                    cur->right->next = cur->next->left;
                }
            cur = cur->next;
            }
            left = left->left;
        }
        return root;
    }
};
```
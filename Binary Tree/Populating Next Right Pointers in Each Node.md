
#CST101-11-04-2023 
#11-04-2023 

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

**Input:** root = `[1,2,3,4,5,6,7]`
**Output:** `[1,#,2,3,#,4,5,6,7,#]`
**Explanation:** Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

**Example 2:**

**Input:** root = []
**Output:** []

**Constraints:**

-   The number of nodes in the tree is in the range `[0, 212 - 1]`.
-   `-1000 <= Node.val <= 1000`

**Follow-up:**

-   You may only use constant extra space.
-   The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.


```cpp
class Solution {
public:
    Node* connect(Node* root) {
        Node* temp = root;
        if(root == NULL)
            return root;
        queue<Node*>q;
        q.push(temp);
        while(!q.empty()){
            size_t size = q.size();
            Node* prev = NULL;
            for(int i = 0; i < size; ++i){
                temp = q.front();
                q.pop();
                if(prev == NULL)
                    prev = temp;
                else{
                    prev->next = temp;
                    prev = temp;
                }
                if(temp->left)
                    q.push(temp->left);
                if(temp->right)
                    q.push(temp->right);
            }
        }
        return root;
    }
};
```



```cpp
class Solution {
public:
    Node* connect(Node* root){
        if(!root) return root;
        dfs(root->left, root->right);
        return root;
    }

    void dfs(Node* left, Node* right){
        if(!left) return;
        left->next = right;
        dfs(left->left, left->right);
        dfs(left->right, right->left);
        dfs(right->left, right->right);
    }
};
```


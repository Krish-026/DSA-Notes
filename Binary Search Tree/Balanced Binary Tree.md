#30-03-2023 









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
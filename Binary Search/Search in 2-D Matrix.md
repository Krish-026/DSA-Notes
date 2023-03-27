
You are given an `m x n` integer matrix `matrix` with the following two properties:

-   Each row is sorted in non-decreasing order.
-   The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` _if_ `target` _is in_ `matrix` _or_ `false` _otherwise_.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = `[[1,3,5,7],[10,11,16,20],[23,30,34,60]]`, target = 3
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = `[[1,3,5,7],[10,11,16,20],[23,30,34,60]]`, target = 13
**Output:** false

**Constraints:**

-   `m == matrix.length`
-   `n == matrix[i].length`
-   `1 <= m, n <= 100`
-   `-104 <= matrix[i][j], target <= 104`

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        if(matrix[0][0] == target or matrix[m-1][n-1] == target) return true;
        int i = 0, j = n-1;
        while(i < m and j >= 0){
            if(matrix[i][j] == target) return true;
            else if(matrix[i][j] > target) --j;
            else ++i;
        }
        return false;
    }

};
```

## Another Approach

Use binary search.

n * m matrix convert to an array => matrix  `[x]  [y] `=> a `[x * m + y]`

an array convert to n * m matrix => a`[x]` =>matrix`[x / m]`  `[x % m]`;

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int> > &matrix, int target) {
        int n = matrix.size();
        int m = matrix[0].size();
        int l = 0, r = m * n - 1;
        while (l != r){
            int mid = (l + r - 1) >> 1;
            if (matrix[mid / m][mid % m] < target)
                l = mid + 1;
            else 
                r = mid;
        }
        return matrix[r / m][r % m] == target;
    }
};
```
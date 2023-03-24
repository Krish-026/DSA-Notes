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

n * m matrix convert to an array => matrix  [x]  [y] => a [x * m + y]

an array convert to n * m matrix => a[x] =>matrix[x / m]  [x % m];

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
https://leetcode.com/problems/01-matrix/

#25-04-2023 
#CST101-25-04-2023 



Given an `m x n` binary matrix `mat`, return _the distance of the nearest_ `0` _for each cell_.

The distance between two adjacent cells is `1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)

**Input:** mat = `[[0,0,0],[0,1,0],[0,0,0]]`
**Output:** `[[0,0,0],[0,1,0],[0,0,0]]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/04/24/01-2-grid.jpg)

**Input:** mat = `[[0,0,0],[0,1,0],[1,1,1]]`
**Output:** `[[0,0,0],[0,1,0],[1,2,1]]`

**Constraints:**

-   `m == mat.length`
-   `n == mat[i].length`
-   `1 <= m, n <= 104`
-   `1 <= m * n <= 104`
-   `mat[i][j]` is either `0` or `1`.
-   There is at least one `0` in `mat`.


```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        queue<pair<int, pair<int,int>>>q;
        int m = mat.size(), n = mat[0].size();
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(mat[i][j] == 0)
                q.push({0, {i, j}});
            }
        }

        int X[] = {-1, 0, 1, 0};
        int Y[] = {0, 1, 0, -1};
        vector<vector<int>>ans(m, vector<int>(n, 0));
        while(!q.empty()){
            auto[level, pq] =  q.front();
            auto[row, col] = pq;
            q.pop();
            for(int i = 0; i < 4; ++i){
                int nRow = X[i] + row;
                int nCol = Y[i] + col;
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n
                    and mat[nRow][nCol] == 1 ){
                        ans[nRow][nCol] = level+1;
                        mat[nRow][nCol] = 2;
                        q.push({level + 1, {nRow, nCol}});
                    }
            }
        }
        return ans;
    }
};
```

```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        queue<pair<int, pair<int,int>>>q;
        int m = mat.size(), n = mat[0].size();
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(mat[i][j] == 0)
                q.push({0, {i, j}});
            }
        }

        int X[] = {-1, 0, 1, 0};
        int Y[] = {0, 1, 0, -1};
        vector<vector<int>>ans(m, vector<int>(n, 0));
        while(!q.empty()){
            auto[level, pq] =  q.front();
            auto[row, col] = pq;
            q.pop();
            for(int i = 0; i < 4; ++i){
                int nRow = X[i] + row;
                int nCol = Y[i] + col;
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n
                    and mat[nRow][nCol] == 1 and ans[nRow][nCol] == 0){
                        ans[nRow][nCol] = level+1;
                        // mat[nRow][nCol] = 2;
                        q.push({level + 1, {nRow, nCol}});
                    }
            }
        }
        return ans;
    }
};
```


```cpp
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        
        int m = mat.size(), n = mat[0].size();
        vector<vector<int>>dp(m, vector<int>(n, 1e8+100));
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(mat[i][j] == 0){
                    dp[i][j] = 0;
                }
            }
        }

        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(mat[i][j] == 1){
                    if(i > 0) dp[i][j] = min(dp[i][j], 1 + dp[i-1][j]);
                    if(j > 0) dp[i][j] = min(dp[i][j], 1 + dp[i][j-1]);
                }
            }
        }

        for(int i = m-1; i >= 0; --i){
            for(int j = n-1; j >= 0; --j){
                if(mat[i][j] == 1){
                    if(i < m-1) dp[i][j] = min(dp[i][j], 1 + dp[i+1][j]);
                    if(j < n - 1) dp[i][j] = min(dp[i][j], 1 + dp[i][j+1]);
                }
            }
        }
        return dp;
    }
};
```


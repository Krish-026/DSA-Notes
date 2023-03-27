#27-03-2023
You are given an `m x n` `grid` where each cell can have one of three values:

-   `0` representing an empty cell,
-   `1` representing a fresh orange, or
-   `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return _the minimum number of minutes that must elapse until no cell has a fresh orange_. If _this is impossible, return_ `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

**Input:** grid = `[[2,1,1],[1,1,0],[0,1,1]]`
**Output:** 4

**Example 2:**

**Input:** grid = `[[2,1,1],[0,1,1],[1,0,1]]`
**Output:** -1
**Explanation:** The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

**Example 3:**

**Input:** grid = `[[0,2]]`
**Output:** 0
**Explanation:** Since there are already no fresh oranges at minute 0, the answer is just 0.

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int ans = 0, m = grid.size(), n = grid[0].size();
        queue<pair<int, pair<int, int>>> q;
        vector<vector<bool>> vis(m, vector<bool>(n, false));
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j] == 2){
                    vis[i][j] = true;
                    q.push({0,{i, j}});
                }
            }
        }
        int X[] = {0, -1, 0, 1};
        int Y[] = {-1, 0, 1, 0};
        while(!q.empty()){
            auto[lvl, RC] = q.front();
            auto[row, col] = RC;
            ans = lvl;
            q.pop();
            for(int k = 0; k < 4; ++k){
                int nRow = X[k] + row;
                int nCol = Y[k] + col;
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n and
                    vis[nRow][nCol] == false and grid[nRow][nCol] == 1){
                        vis[nRow][nCol] = true;
                        grid[nRow][nCol] = 2;
                        q.push({lvl+1, {nRow, nCol}});
                    }
            }
        }
        for(auto x: grid){
            for(int num: x){
                if(num == 1) return -1;
            }
        }
        return ans;
    }
};
```

## Optimized

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int ans = 0, m = grid.size(), n = grid[0].size(), fresh = 0;
        queue<pair<int, pair<int, int>>> q;
        vector<vector<bool>> vis(m, vector<bool>(n, false));
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j] == 2){
                    vis[i][j] = true;
                    q.push({0,{i, j}});
                }
                else if(grid[i][j] == 1) ++fresh;
            }
        }
        int X[] = {0, -1, 0, 1};
        int Y[] = {-1, 0, 1, 0};
        while(!q.empty()){
            auto[lvl, RC] = q.front();
            auto[row, col] = RC;
            ans = lvl;
            q.pop();
            for(int k = 0; k < 4; ++k){
                int nRow = X[k] + row;
                int nCol = Y[k] + col;
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n and
                    vis[nRow][nCol] == false and grid[nRow][nCol] == 1){
                        vis[nRow][nCol] = true;
                        --fresh;
                        q.push({lvl+1, {nRow, nCol}});
                    }
            }
        }
        if(fresh == 0) return ans;
        else return -1;
    }
};
```
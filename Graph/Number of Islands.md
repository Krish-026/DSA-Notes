https://leetcode.com/problems/number-of-islands/

#CST101-19-04-2023
#19-04-2023 

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = ```[

  ["1","1","1","1","0"],

  ["1","1","0","1","0"],

  ["1","1","0","0","0"],

  ["0","0","0","0","0"]

]```
**Output:** 1

**Example 2:**

**Input:** grid = ```[

  ["1","1","0","0","0"],

  ["1","1","0","0","0"],

  ["0","0","1","0","0"],

  ["0","0","0","1","1"]

]```
**Output:** 3

**Constraints:**

-   `m == grid.length`
-   `n == grid[i].length`
-   `1 <= m, n <= 300`
-   `grid[i][j]` is `'0'` or `'1'`.




```cpp
class Solution {
private:
    void dfs(vector<vector<char>>& grid, int row, int col){
        grid[row][col] = '2';
        int X[] = {-1, 0, 1, 0};
        int Y[] = {0, 1, 0, -1};
        for(int i = 0; i < 4; ++i){
            int nRow = row + X[i];
            int nCol = col + Y[i];
            if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n
                and grid[nRow][nCol] == '1')
                dfs(grid, nRow, nCol);
        }
    }
public:
    int m , n;
    int numIslands(vector<vector<char>>& grid) {
        int ans = 0;
        m = grid.size(), n = grid[0].size();;
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j] == '1'){
                    dfs(grid, i, j);
                    ++ans;
                }
            }
        }
        return ans;
    }
};
```
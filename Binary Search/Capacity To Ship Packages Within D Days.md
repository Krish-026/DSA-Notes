#27-03-2023 
#CST101-27-03-2023 

Similar Question - [[Minimum Time to Repair Cars]]
A conveyor belt has packages that must be shipped from one port to another within `days` days.

The `ith` package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `days` days.

**Example 1:**

**Input:** weights = `[1,2,3,4,5,6,7,8,9,10]`, days = 5
**Output:** 15
**Explanation:** A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.

**Example 2:**

**Input:** weights = `[3,2,2,4,1,4]`, days = 3
**Output:** 6
**Explanation:** A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4

**Example 3:**

**Input:** weights = ~`[1,2,3,1,1]`~, days = 4
**Output:** 3
**Explanation:**
1st day: 1
2nd day: 2
3rd day: 3
4th day: 1, 1

**Constraints:**

-   `1 <= days <= weights.length <= 5 * 104`
-   `1 <= weights[i] <= 500`

## Code

```cpp
class Solution {
private: 
    bool solve(vector<int>&arr, int limit, int D){
        int count = 1, sum = 0;
        for(int x: arr){
            sum += x;
            if(sum > limit){
                ++count;
                sum = x;
            }
        }
        return count <= D;
    }
public:
    int shipWithinDays(vector<int>& weights, int days) {
        int lo = 0, hi = 0;
        for(int x: weights){
            lo = max(lo, x);
            hi += x;
        }
        int ans = 0;
        while(lo <= hi){
            int mid = lo + (hi - lo)/2;
            if(solve(weights, mid, days)){
                ans = mid;
                hi = mid - 1;
            }
            else lo = mid + 1;
        }
        return ans;
    }
};
```


## BFS

```cpp
class Solution {
private:
    void bfs(vector<vector<char>>&grid, int i, int j){
        int X[] = {-1, 0, 1, 0};
        int Y[] = {0, 1, 0, -1};
        queue<pair<int, int>>q;
        grid[i][j] = '2';
        q.push({i, j});
        while(!q.empty()){
            int row = q.front().first;
            int col = q.front().second;
            q.pop();
            
            for(int i = 0; i < 4; ++i){
                int nRow = row + X[i];
                int nCol = col + Y[i];
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n
                    and grid[nRow][nCol] == '1'){
                        grid[nRow][nCol] = '2';
                        q.push({nRow, nCol});
                    }
            }
            
        }
    }
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
                    bfs(grid, i, j);
                    ++ans;
                }
            }
        }
        return ans;
    }
};
```
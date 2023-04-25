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
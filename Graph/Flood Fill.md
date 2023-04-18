#27-03-2023
An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `color`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `color`.

Return _the modified image after performing the flood fill_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

**Input:** image = `[[1,1,1],[1,1,0],[1,0,1]]`, sr = 1, sc = 1, color = 2
**Output:** `[[2,2,2],[2,2,0],[2,0,1]]`
**Explanation:** From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.

**Example 2:**

**Input:** image = `[[0,0,0],[0,0,0]]`, sr = 0, sc = 0, color = 0
**Output:**` [[0,0,0],[0,0,0]]`
**Explanation:** The starting pixel is already <colored 0, so no changes are made to the image.

```cpp
class Solution {
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int m = image.size(), n = image[0].size();
        vector<vector<bool>>vis(m, vector<bool>(n, false));
        queue<pair<int, int>> q;
        q.push({sr, sc});
        int oldCol = image[sr][sc];
        image[sr][sc] = color;
        int X[] = {0, -1, 0, 1};
        int Y[] = {-1, 0, 1, 0};
        while(!q.empty()){
            auto[row, col] = q.front(); q.pop();
            for(int i = 0; i < 4; ++i){
                int nRow = row + X[i];
                int nCol = col + Y[i];
                if(nRow >= 0 and nRow < m and nCol >= 0 and nCol < n
                    and vis[nRow][nCol] == false and image[nRow][nCol] == oldCol){
                        image[nRow][nCol] = color;
                        vis[nRow][nCol] = true;
                        q.push({nRow, nCol});
                    }
            }
        }
        return image;
    }
};
```
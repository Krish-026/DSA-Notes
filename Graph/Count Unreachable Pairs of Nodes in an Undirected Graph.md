#27-03-2023
You are given an integer `n`. There is an **undirected** graph with `n` nodes, numbered from `0` to `n - 1`. You are given a 2D integer array `edges` where `edges[i] = [ai, bi]` denotes that there exists an **undirected** edge connecting nodes `ai` and `bi`.

Return _the **number of pairs** of different nodes that are **unreachable** from each other_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/05/05/tc-3.png)

**Input:** n = 3, edges = `[[0,1],[0,2],[1,2]]`
**Output:** 0
**Explanation:** There are no pairs of nodes that are unreachable from each other. Therefore, we return 0.


# Intuition

We have total n nodes so if one component has k nodes then we will have k * (n-k-total)(where total is number of nodes we have already visited) pairs which are unreachable

# Approach

Run a DFS algorithm for count number of nodes in one compoenent and store that nodes in a vector keep one variable res for storing result and one other var int total = 0 to keep track of nodes we have already visited and then count pairs as per above formula  
update total count

# Complexity

-   Time complexity:

The above algorithm calls DFS, finds reverse of the graph and again calls DFS. DFS takes O(V+E) for a graph represented using adjacency list.

-   Space complexity:

O(V) as we are using a stack to store the vertices.  
O(N) for making temp array

```cpp
class Solution {

private:

    void dfs(vector<int>adj[], int src, vector<bool>&visited, long long& count){

        if(visited[src]) return;

        visited[src] = true;

        ++count;

        for(int x: adj[src]){

            dfs(adj, x,visited, count);

        }

    }

public:

    long long countPairs(int n, vector<vector<int>>& edges) {

        vector<int>adj[n];

        for(auto it: edges){

            adj[it[0]].push_back(it[1]);

            adj[it[1]].push_back(it[0]);

        }

        long long count = 0;

        vector<bool>visited(n, false);

        vector<long long>arr;

        for(int i = 0; i < n; ++i){

            if(!visited[i]){

                count = 0;

                dfs(adj, i, visited, count);

                arr.push_back(count);

            }

        }

        long long ans = 0;

        for(auto x: arr){

            ans += (n-x)*x;

        }

        return (ans>>1);

    }

};
```

## Another Approach

```cpp
void dfs(int node, int par, vector<vector < int>> &adj, vector< int > &vis, int &k)
    {
        vis[node] = 1;
        k++;
        for (auto it: adj[node])
        {
            if (!vis[it])
            {
                dfs(it, node, adj, vis, k);
            }
        }
    }
        long long countPairs(int n, vector<vector < int>> &edges)
        {
            vector<vector < int>> adj(n);
            for (auto it: edges)
            {
                adj[it[0]].push_back(it[1]);
                adj[it[1]].push_back(it[0]);
            }
            vector<int> vis(n, 0);
            ll ans = 0, tot = 0;
            for (int i = 0; i < n; i++)
            {
                int k = 0;
                if (!vis[i])
                {
                    dfs(i, -1, adj, vis, k);
                }
                ans += k *(n - k - tot);
                tot += k;
            }
            return ans;
        }
```
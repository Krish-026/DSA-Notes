#27-03-2023
There are `n` cities numbered from `0` to `n - 1` and `n - 1` roads such that there is only one way to travel between two different cities (this network form a tree). Last year, The ministry of transport decided to orient the roads in one direction because they are too narrow.

Roads are represented by `connections` where `connections[i] = [ai, bi]` represents a road from city `ai` to city `bi`.

This year, there will be a big event in the capital (city `0`), and many people want to travel to this city.

Your task consists of reorienting some roads such that each city can visit the city `0`. Return the **minimum** number of edges changed.

It's **guaranteed** that each city can reach city `0` after reorder.

```cpp
class Solution {

private:

    void dfs(vector<int>adj[], int src, vector<bool>&vis, int& count){

        vis[src] = true;

        for(auto x: adj[src]){

            if(!vis[abs(x)]){

                if(x > 0)

                    ++count;

                dfs(adj, abs(x), vis, count);

            }  

        }

    }

public:

    int minReorder(int n, vector<vector<int>>& connections) {

        vector<int>adj[n];
    
        //for every city store the adjacent city along with direction 
        //to store the direction we use positive indicating a road from a to b for a
        //we use negative indicating there is a road from b to a for a

        for(auto x: connections)

            adj[x[0]].push_back(x[1]), adj[x[1]].push_back(-x[0]);

        vector<bool>visited(n, false);


        //start dfs from city  0 
        //when ever you found a positive then it need to be reversed

        int count = 0;

        dfs(adj, 0, visited, count);

        return count;

    }

};
```

## Another Approach

The idea is to do a DFS traversal starting from node 0. For nodes other than 0, we check the parent who called DFS on it, and if it doesn't have an outgoing edge to the parent, we increment the answer. We don't really need to reverse any edge.

```cpp
void dfs(int idx,int caller,vector<vector<int>> &adjList,vector<vector<int>> &outgoing,vector<bool> &visited,int &ans){
        visited[idx]=true;
        if(caller!=-1){     //if the city number is not 0
            //check if there is an outgoing edge from current node to it's parent node (who called dfs on this node)
            //if there is no outgoing edge, we'll have to reorient this edge
            if(find(outgoing[idx].begin(),outgoing[idx].end(),caller)==outgoing[idx].end())
                ans++;
        }
        for(auto i: adjList[idx]){
            if(!visited[i]){
                dfs(i,idx,adjList,outgoing,visited,ans);
            }
        }
 }
int minReorder(int n, vector<vector<int>>& connections) {
        int ans=0;
        vector<vector<int>> adjList(n);     //doesn't cares about direction
        vector<vector<int>> outgoing(n);    //list of outgoing nodes from a node
        vector<bool> visited(n,false);       
        for(auto i: connections){
            adjList[i[0]].push_back(i[1]);
            adjList[i[1]].push_back(i[0]);
            outgoing[i[0]].push_back(i[1]);
        }
        dfs(0,-1,adjList,outgoing,visited,ans);     //start dfs from node 0 
        return ans;
 }
```

The caller argument in the dfs function denotes the node who called dfs on the current node, i.e. it's parent. We intially call dfs on node 0 with caller=-1 as it doesn't have any parent to which it wants to reach.

#27-03-2023
There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

**Input:** isConnected = `[[1,1,0],[1,1,0],[0,0,1]]`
**Output:** 2

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

**Input:** isConnected = `[[1,0,0],[0,1,0],[0,0,1]]`
**Output:** 3

**Constraints:**

-   `1 <= n <= 200`
-   `n == isConnected.length`
-   `n == isConnected[i].length`
-   `isConnected[i][j]` is `1` or `0`.
-   `isConnected[i][i] == 1`
-   `isConnected[i][j] == isConnected[j][i]

Code

```cpp
class Solution {

private:

    void dfs(vector<int>adj[], int src, vector<bool>&vis){

        vis[src] = true;

        for(int x: adj[src]){

            if(!vis[x]) dfs(adj, x, vis);

        }

    }

public:

    int findCircleNum(vector<vector<int>>& isConnected) {

        int n = isConnected.size();

        vector<int>adj[n];

        for(int i = 0; i < n; ++i){

            for(int j = 0; j < n; ++j){

                if(isConnected[i][j] and i != j){

                    adj[i].push_back(j);

                    adj[j].push_back(i);

                }

            }

        }

        int count = 0;

        vector<bool>visited(n, false);

        for(int i = 0; i < n; ++i){

            if(!visited[i]){

                ++count;

                dfs(adj, i, visited);

            }

        }

        return count;

    }

};
```


## Another Approach

- Learn Union Path Concept

**Let's say 1 and 2 are friend , and 2 and 3 are also friend  
Then indirectly 1 and 3 are also friends. We can say that 1,2,3 are in same group.**

How we will deal with it in UNION:

WE have given **n * n matrix** , then **maximum number of group will be n**, if nobody is friend of none.

Lets Say n=5  
Now we mark all of them initially with -1, because at starting all are alone, all are self leader.  
**At the end we will find -1 for those index which will be leader of any group**

_INDEX :  ```[ 1 , 2 ,3 ,4 , 5]```
VALUES:```[-1,-1,-1,-1,-1]```

Now **1 is friend of 2**, mark **2** as a leader , how can we do this, simple ,**point index 2 from 1**  
_INDEX : `[ 1 , 2 ,3 ,4 , 5]`
VALUES: ``[ 2,-1,-1,-1, -1]  ``
Here how we will find leader ,start from index 1

**1 is pointing 2 , 1->2  
2 is pointing -1, 2 is leader of group**

Now **2 is friend of 3**, Now **point 2 at index 3**  
_INDEX : `[ 1 , 2 ,3 ,4 , 5] `
VALUES: `[ 2 , 3,-1,-1, -1]`

**1 is pointing 2 , 1->2  
2 is pointing 3 , 2->3  
3 is pointing -1 , 3 is leader of group**

Now if we start finding **leader of 1 and 2** , then **3** is the leader (**COMMON LEADER: SAME GROUP**)

Now **4 is friend of 5**, Now **point 4 at index 5**  
_INDEX : `[ 1 , 2 ,3 ,4 , 5]`
VALUES: `[ 2 , 3,-1, 5, -1]`

At the end just count total number of parent nodes whose value is -1.  
Now we have **two** groups **{1,2,3}** and **{4,5}** , NOW go to solution line by line :)

```cpp
class Solution {
public:
    
    //It will be use to store groups
    vector<int> v;
    
    //Find the leader of any group in which x lies
    //if not lie in any group then it is self leader
    int parent(int x)
    {
        //self leader
        if(v[x]==-1) return x; 
        //find the leader of self parent
        return v[x]=parent(v[x]);
    }
    
    //Adding 2 friends in a group
    void _union(int a,int b)
    {
        //find the leader of both a and b
        int p_a=parent(a),p_b=parent(b);
        
        //if already in same group, i.e leader of both of them are same then return
        if(p_a==p_b) return; 
        /*
         if both of them are from different group then add both the groups 
         and make a single common group
         We can do this by -> leader of 1st group is member of 2nd group 
         and now main leader of whole group is leader of 2nd member
        */ 
        v[p_a]=p_b; //v[p_a] will store the index of leader of whole group
    }
    
    int findCircleNum(vector<vector<int>>& M) { 
        int n=M.size();
        v=vector<int> (n,-1);//there will be maximum n group, mark all as a leader
        
        //making group
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(M[i][j])  //if i is friend of j, add them in a group
                { 
                    //if i is in any group then add j in that group
                    //or vice-versa
                    _union(i,j);  //Add them in a group
                }
            }
        }
        int c=0; 
        
        //counting group
        for(int i=0;i<n;i++)
        {
            if(v[i]==-1) c++; //counting total number of parents
        }
        return c; 
    }
};
```
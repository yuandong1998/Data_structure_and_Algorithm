# [面试题 04.01. 节点间通路](https://leetcode-cn.com/problems/route-between-nodes-lcci/)

**Question**

![](https://i.bmp.ovh/imgs/2021/02/47404f7c8653bb20.png)


## Method1

**Idea**

DFS，通过`vector<unordered_set<int>> graph`构建邻接矩阵。然后采用DFS。`graph_adj`和`visited`设置为全局变量。



**Code**

```C++
class Solution {
public:
    bool findWhetherExistsPath(int n, vector<vector<int>>& graph, int start, int target) {
        if(start==target){
            return true;
        }
        //构建邻接矩阵
        graph_adj=vector<unordered_set<int>>(n);
        visited=vector<bool>(n,false);
        for(auto x:graph){
            graph_adj[x[0]].insert(x[1]);
        }
        return dfs(start,target);
    }

    bool dfs(int s,int e){
        if(s==e){return true;}
        visited[s] = true;
        for (const auto& neighbor : graph_adj[s]) {
            if (visited[neighbor]) {
                continue;
            }
            if (dfs(neighbor, e)) {
                return true;
            }
        }
        return false;
    }
private:
    vector<bool> visited;
    vector<unordered_set<int>> graph_adj;
};
```



**Complexity Analysis**

* Time Complexity：$O(N^2)$。
* Space Complexity：$O(N^2)$。
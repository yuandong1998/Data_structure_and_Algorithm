# [980. Unique Paths III](https://leetcode-cn.com/problems/unique-paths-iii/)



**Q:**On a 2-dimensional `grid`, there are 4 types of squares:

* `1` represents the starting square.  There is exactly one starting square.
* `2` represents the ending square.  There is exactly one ending square.
* `0` represents empty squares we can walk over.
* `-1` represents obstacles that we cannot walk over.

Return the number of 4-directional walks from the starting square to the ending square, that **walk over every non-obstacle square exactly once.**



## Solution1

**Idea:** 采用**回溯算法**， 先统计有多少个格子需要去走，走到终点时判断是否走完了所有格子。每次走一个格子将格子设为`-1`，防止下次再走。通过如下代码实现上下左右四个方向。

```
//上下左右四个方向
vector<int> sec_r={0,0,-1,1};
vector<int> sec_c={1,-1,0,0};
...
for(int k=0;k<=3;k++){
	int tmp_r=cur_r+sec_r[k];
	int tmp_c=cur_c+sec_c[k];
}        
```



**Code:**

```C++
class Solution {
public:
    int res=0;//统计有多少种路径
    int start_r=0,start_c=0,end_r=0,end_c=0;//起始节点和终止节点
    //上下左右四个方向
    vector<int> sec_r={0,0,-1,1};
    vector<int> sec_c={1,-1,0,0};
    int r_len=0,c_len=0;

    void track_back(int cur_r,int cur_c,vector<vector<int>>& grid,int todo){
        todo--;
        if(cur_c==end_c && cur_r==end_r){//到达终点
            if(todo==0){//满足条件
                res++;
            }
            return;
        }
        int f=grid[cur_r][cur_c];
        grid[cur_r][cur_c]=-1;//走这一格
        for(int k=0;k<=3;k++){
            int tmp_r=cur_r+sec_r[k];
            int tmp_c=cur_c+sec_c[k];
            if(tmp_r>=0 && tmp_r<r_len && tmp_c>=0 && tmp_c<c_len){
                if(grid[tmp_r][tmp_c]%2==0){
                    track_back(tmp_r,tmp_c,grid,todo);
                }
            }
        }
        grid[cur_r][cur_c]=f;

    }
    int uniquePathsIII(vector<vector<int>>& grid) {

        int todo=0;//需要走的格子
        r_len=grid.size();//行数
        c_len=grid[0].size();//列数
        for(int r=0;r<r_len;r++){
            for(int c=0;c<c_len;c++){
                if(grid[r][c]!=-1) todo++;//统计需要走的格子
                if(grid[r][c]==1){start_r=r;start_c=c;}//找到起始点
                if(grid[r][c]==2){end_r=r;end_c=c;}//找到终点
            }
        }
        track_back(start_r,start_c,grid,todo);
        return res;

    }
};
```



**Complexity Analysis**

* Time Complexity: $O(4^{R*C})$ ，我们可以找到一个更加精确的界限。
* Space Complexity: $O(RC)$
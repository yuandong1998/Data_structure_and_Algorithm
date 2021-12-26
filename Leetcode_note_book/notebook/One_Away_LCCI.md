# [One Away LCCI](https://leetcode-cn.com/problems/one-away-lcci/)

**Question:**

<img src="C:\Users\13775\AppData\Roaming\Typora\typora-user-images\image-20210127135658055.png" alt="image-20210127135658055" style="zoom: 67%;" />



## Method1

**Idea:**

dynamic programming(DP).`dp[i][j]`表示first的前`i`部分edit为second的前`j`部分需要的编辑次数。

```[]
init：dp[0][0]=0,dp[i][0]=i,dp[0][j]=[j].
trans：dp[i][j]=min(min(dp[i-1][j]+1,dp[i][j-1]+1),dp[i-1][j-1]); if first[i]==second[j],
		dp[i][j]=min(min(dp[i-1][j]+1,dp[i][j-1]+1),dp[i-1][j-1]+1) if first[i]!=second[j]
result:dp[i][j]==1 or 0
```



**Code:**

```C+=
class Solution {
public:
    bool oneEditAway(string first, string second) {
        int fl=first.size(),sl=second.size();
        if(abs(fl-sl)>1) {return false;}
        vector<vector<int>> dp(fl+1,vector<int>(sl+1,0));
        for(int i=1;i<=fl;i++) {
            dp[i][0]=i;
        }
        for(int i=1;i<=sl;i++) {
            dp[0][i]=i;
        }
        for(int i=1;i<=fl;i++){
            for(int j=1;j<=sl;j++){
                if(first[i-1]==second[j-1]){
                    dp[i][j]=min(min(dp[i-1][j]+1,dp[i][j-1]+1),dp[i-1][j-1]);
                }else{
                    dp[i][j]=min(min(dp[i-1][j]+1,dp[i][j-1]+1),dp[i-1][j-1]+1);
                }
            }
        }
        return dp[fl][sl]<=1;

    }
};
```



**Complexity analysis**

* time complexity:$O(M*N)$
* space complexity:$O(M*N)$

**others**

```
二维vector初始化：
vector<vector<int>> dp(fl+1,vector<int>(sl+1,0));
```



## Method2

**Idea:**

只需要判断是否小于一次edit，不用计算DP，见如下code，`(s1 - s2)`表示两个的长度大小差，为0或1，`edit`表示编辑的次数。表示如果有一处不相等了，我们可以跳过它，如果$s1-s2==1$则是错开一位，如果相等则是不错开。



**Code**

```C++
class Solution {
public:
    bool oneEditAway(string first, string second) {
        int s1 = first.size(), s2 = second.size();
        if (abs(s1 - s2) > 1) return false;
        if (s1 < s2) return oneEditAway(second, first);
        for (int i = 0, edit = 0; i < s1; i++) {
            if (first[i] != second[i - (s1 - s2) * edit] && ++edit > 1) {
                return false;
            }
        }
        return true;
    }
};
```



**Complexity analysis**

* time complexity:$O(max(M,N))$
* space complexity:$O(1)$


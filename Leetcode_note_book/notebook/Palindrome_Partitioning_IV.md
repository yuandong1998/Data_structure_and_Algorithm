# [回文串分割 IV](https://leetcode-cn.com/problems/palindrome-partitioning-iv/)

Question

![](https://i.bmp.ovh/imgs/2021/02/c27239ec3769a79d.png)



## Method1

**Idea**

动态规划。我们用bool型dp[i][j]表示字符串以i为开头，j为结尾的字符串是否非回文子串。判断的边界是dp[i][i]作为单字符全部都是回文子串。
$$
d p[i][j]=\left\{\begin{array}{ll}
d p[i+1][j-1] & \text { if } s[i]=s[j] \\
0 & \text { if } s[i] \neq s[j]
\end{array}\right.
$$


**Code**

```C++
const int maxn = 2010;
bool dp[maxn][maxn];

class Solution {
public:
    bool checkPartitioning(string s) {
        memset(dp, 0, sizeof(dp));
        int n = s.length();
        for(int i = 0; i < n; i++){
            dp[i][i] = 1;
            if(i < n - 1){
                if(s[i]==s[i+1])dp[i][i+1] = 1;
            }
        }
        for(int L = 3; L <= n; L++){
            for(int i = 0; i + L - 1 < n; i++){
                int j = i + L - 1;
                if(s[i]==s[j] && dp[i+1][j-1]){
                    dp[i][j] = 1;
                }
            }
        }
        for(int s = 1; s <= n - 2; s++)
            for(int e = s; e <= n - 2; e++)
                if(dp[0][s-1]&&dp[s][e]&&dp[e+1][n-1])
                    return true;
        return false;
    }
};
```



**Complexity Analysis:**

* Time Complexity :$O(n^2)$
* Space Complexity : $O(n^2)$



## Reference

[1] [动态规划 检查回文子串 O(n^2) - 回文串分割 IV - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/palindrome-partitioning-iv/solution/dong-tai-gui-hua-jian-cha-hui-wen-zi-chu-y6og/)
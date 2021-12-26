# KMP算法

Knuth-Morris-Pratt 算法，简称 KMP 算法，由 Donald Knuth、James H. Morris 和 Vaughan Pratt 三人于 1977年联合发表。

Knuth-Morris-Pratt 算法的核心为前缀函数，记作 $\pi(i)$，其定义如下：对于长度为 m 的字符串 s，其前缀函数 $\pi(i)(0 \leq i < m)$表示 s 的子串 $s[0:i]$的最长的相等的真前缀与真后缀的长度。特别地，如果不存在符合条件的前后缀，那么 $\pi(i) = 0$。其中真前缀与真后缀的定义为不等于自身的的前缀与后缀。有了前缀函数，我们就可以快速地计算出模式串在主串中的每一次出现。



**如何求解前缀函数**

几个前缀函数的性质:

* $\pi(i) \leq \pi(i-1) + 1$
* 如果 $s[i]=s[\pi(i-1)]$，那么 $\pi(i)=\pi(i-1)+1$.

所以我们要找到最大的`j`，满足$s[0:j-1]=s[i-j:i-1]$，且$s[i]=s[j]$。

由$\pi(i-1)$的定义可知：$s[0:\pi(i-1)-1]=s[i-\pi(i-1):i-1]$，那么$j=\pi(i-1)$符合第一个要求，如果$s[i]=s[\pi(i-1)]$，那么就可以确定$\pi(i)$。

如果$s[i]\neq s[\pi(i-1)]$，那么$\pi(i)\leq \pi(i-1)$，我们要找最大的`j`满足$s[0:j−1]=s[π(i−1)−j:π(i−1)−1]$，且$s[i]=s[\pi(i-1)]$。如此循环。



## Code

```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.size(), m = needle.size();
        if (m == 0) {
            return 0;
        }
        //构建pi()
        vector<int> pi(m);
        //i从1开始，j从0开始。
        for (int i = 1, j = 0; i < m; i++) {
            while (j > 0 && needle[i] != needle[j]) {
                j = pi[j - 1];
            }
            if (needle[i] == needle[j]) {
                j++;
            }
            pi[i] = j;
        }
        
        //匹配
        for (int i = 0, j = 0; i < n; i++) {
            //如果不匹配 j=pi[j-1]
            while (j > 0 && haystack[i] != needle[j]) {
                j = pi[j - 1];
            }
            if (haystack[i] == needle[j]) {//如果匹配 i++ j++
                j++;
            }
            if (j == m) { //满足条件
                return i - m + 1;
            }
        }
        return -1;
    }
};
```









## Reference

[1] [LeetCode-Solution](https://leetcode-cn.com/problems/implement-strstr/solution/shi-xian-strstr-by-leetcode-solution-ds6y/)

